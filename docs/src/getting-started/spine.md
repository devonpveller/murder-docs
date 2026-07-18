# Spine Skeletal Animation

Murder supports [Spine](https://esotericsoftware.com/) skeletal animation as a first-class asset type, alongside its frame-based Aseprite sprites. A Spine skeleton is imported as a `SpineAsset`, placed in a scene via a `SpineComponent`, and driven at runtime by a small set of systems — mirroring the `SpriteAsset`/`SpriteComponent`/`SpriteRenderSystem` pipeline you already know.

This guide covers importing a skeleton, rendering and animating it, sizing it, crossfading animations, and attaching props to bones ("sockets").

## Setup

The Spine runtime (`spine-csharp` plus a thin FNA renderer) is vendored through the `spine-runtimes` git submodule and compiled by the `Murder.Spine` project. When cloning Murder — or updating it as a submodule in your own game — make sure the nested submodule is checked out:

```sh
git submodule update --init --recursive
```

If `spine-runtimes` is missing, every Spine source file fails to compile with *"The type or namespace name 'Spine' could not be found"*.

## Importing a skeleton

Export your skeleton from the Spine editor as usual — a skeleton descriptor (`.json` or `.skel`), an `.atlas`, and its texture page(s). Drop all of them into your project's `resources/spine/` folder (subfolders are fine, e.g. `spine/spineboy/`).

On the next import, the `SpineImporter` copies the files through as-is (Spine ships its own pre-packed atlas, so unlike sprites they are *not* run through Murder's texture packer) and creates one `SpineAsset` per skeleton descriptor. The asset's GUID is derived deterministically from the skeleton's path, so it stays stable across imports and machines — a `SpineComponent` that references it never goes stale.

## Placing a skeleton in a scene

Add a `SpineComponent` to an entity (it requires a `PositionComponent`) and set:

- **Skeleton** — the `SpineAsset` to draw.
- **Animation** — picked from a dropdown of the skeleton's animations (once a skeleton is assigned). Animations are skeleton-wide, not per-skin.
- **Loop** — whether that animation loops.
- **Target Sprite Batch** — which batch layer the skeleton draws into, controlling its draw order relative to other visuals (same idea as `SpriteComponent`).

### Required systems

Skeletons are driven by ECS systems, so the world you are playing must include them in its **Systems** list (a world only runs systems it lists — see the systems tab of the world editor):

- `SpineAnimationSystem` — resolves the asset, builds the per-entity skeleton, and advances the pose each frame.
- `SpineRenderSystem` — draws the posed skeleton.
- `DynamicInCameraSystem` — flags on-screen entities as visible; **the two systems above only run for entities it has marked in-camera**, so a Spine entity will silently never animate or draw without it.
- `SpineBoneFollowerSystem` — only needed if you use bone-follower sockets (below).

> The plain **Play** button always launches the scene set in **Game Profile → Starting Scene**, not whichever world tab is currently open. If Play reports a world "has no systems", check that setting points at the world you actually configured.

## Sizing a skeleton

Spine authors skeletons in their own units, which rarely match a game's pixel scale, so scaling happens at two levels — the same split sprites use:

1. **`SpineAsset.BaseScale`** — an asset-level *import scale* applied to every instance of the skeleton, editable in the Spine asset editor. Set this once so the skeleton is roughly the right size everywhere (the role an import scale plays in Unity/Unreal).
2. **`ScaleComponent`** — Murder's standard per-entity scale, honored by the Spine renderer exactly as it is for sprites. It multiplies on top of `BaseScale` and is per-axis, so a negative X mirrors the skeleton for facing direction. Use the editor's scale gizmo, or set it from gameplay code.

A `BaseScale` of `0` is treated as native (`1`) so a skeleton is never accidentally scaled to nothing.

`BaseScale` is an *import attribute*: it lives on the asset, is tuned in the Spine asset editor, and is preserved across reimports (the importer will not reset it when it regenerates the asset).

> **Animation blending is planned, not yet built.** Changing a `SpineComponent`'s animation is currently an instant cut. Continuous weighted blending of several animations — a 2D blend space with a movable puck, driven from gameplay — is the planned model (see `_agent/_plans/spine-integration/blend-space.md`). This guide will document it when it ships.

## Skins

If a skeleton defines Spine **skins** (character variants, or mix-and-match equipment — a base plus hair, clothes, accessories), pick them per entity on the `SpineComponent`: its inspector shows a checklist of the skeleton's skins. Tick one for a single skin, or several to **combine** them in order (base + pieces) — the mix-and-match case. None ticked uses the skeleton's default setup. The Spine asset editor shows how many skins a skeleton defines (hover for the list). Skeletons with only a default skin show no checklist.

## Tint and fade

A Spine skeleton honors Murder's standard **`TintComponent`** (a color multiplied over the whole skeleton) and **`AlphaComponent`** (fade), the same components sprites use — so damage flashes, status colors, and fade-in/out written for sprites work unchanged on a Spine entity. With neither present the skeleton renders at its authored colors. (This tints the whole skeleton; per-slot coloring is planned.)

## Animation events

Events authored in Spine (footsteps, hit frames, cast points, …) dispatch the **same** Bang messages that Aseprite animations do, so gameplay reacts to them identically regardless of the animation source:

- Each Spine event sends an `AnimationEventMessage` carrying the event's name — read it with `message.Is("footstep")` in a reactive system or state machine, exactly as for a sprite tag event.
- Each time an animation reaches its end, an `AnimationCompleteMessage` is sent — `Sequence` when a non-looping animation finishes, `Single` at each loop of a looping one.

Because these are the existing message types, existing listeners work with Spine unchanged — including `AnimationEventBroadcasterComponent`, which re-broadcasts an entity's animation events to other entities. Events fire only during live playback, not while scrubbing in the editor. (Spine event payloads — `Int`/`Float`/`String` values — aren't carried yet; the message holds the event name, matching sprites.)

Events are authored **in Spine**, per animation, on each animation's timeline — Murder reads them, it doesn't re-author them. The Spine asset editor shows the selected animation's events as markers on its timeline (hover for name and time), so you can see what fires and when.

### Binding responses (no code)

Responses go through Murder's general **`EventListenerEditorComponent`** — the same data-driven event→response system sprites use — so a Spine event can trigger a sound *and* any interactions, and it grows as that system grows. Spine only sources the event and fires it; the response lives on the listener.

The `SpineComponent` inspector lists the skeleton's authored events (as `animation: event`, e.g. `walk: footstep`). Click **Add to Event Listener** next to one and it's linked into the entity's `EventListenerEditorComponent` (added if absent) by event name; author the sound/interactions there. At runtime `EventListenerSystem` fires the bound response when the event occurs — no Spine-specific listener, and the sprite path is untouched. A prefab carrying a `SpineComponent` plus its Event Listener is a reusable, self-contained character. (`EventListenerSystem` must be in the world's systems list.)

## Previewing in the editor

Opening a `SpineAsset` opens the Spine asset editor, which shows:

- A live viewport of the skeleton, driven by the same systems used at runtime.
- The animation list — click any animation to preview it.
- A scrubber timeline — pause and drag to scrub to an exact point in an animation.
- The bone hierarchy.
- Event markers on the selected animation's timeline (read-only; authored in Spine).
- A **Skins** section (when the skeleton has variants) — tick skins to preview them on the skeleton, combined, without wiring up an entity.
- The **Import scale** control, which updates the preview live.

## Bone-follower sockets

To attach a prop, weapon, or effect to a moving bone (a "socket"), add a `SpineBoneFollowerComponent` to the follower entity. It requires a `GuidToIdTargetComponent` (added automatically), which is how you point at the skeleton entity from the editor — pick the target in the scene the same way as any other entity reference. Then set:

- **Bone** — picked from the *target* skeleton's bone hierarchy (an expandable tree of the skeleton the follower points at), rather than typed. Falls back to a text field if the target skeleton can't be resolved.
- **Offset** — an additional pixel offset on top of the bone's world position.

Each frame, `SpineBoneFollowerSystem` (which runs after `SpineAnimationSystem`, so the pose is already resolved) moves the follower to the bone's world position. An unknown bone name logs an error and leaves the follower in place rather than throwing.

## What's supported

The integration currently covers importing, rendering, single-track animation playback, animation events and completion routed into Murder's message system, per-asset import scale, per-entity scale/flip, whole-skeleton tint and fade, single and combined skins, editor preview and scrubbing, the bone hierarchy view, and bone-follower sockets. Further authoring and runtime-control features — a 2D blend space for continuous weighted blending, per-slot tint, bounding-box hitboxes, and constraint control — are planned.

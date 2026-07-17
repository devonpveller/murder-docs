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
- **Animation** — the name of the animation to play on track 0, exactly as authored in Spine.
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

## Crossfading animations

By default, changing a `SpineComponent`'s animation is an instant cut. Set **`SpineAsset.DefaultMix`** (seconds) in the Spine asset editor to crossfade between animations instead — so transitions like idle → walk → run ease between poses. `0` keeps the instant cut. This is a global default; a per-animation-pair mix table can be layered on top later.

`BaseScale` and `DefaultMix` are *import attributes*: they live on the asset, are tuned in the Spine asset editor, and are preserved across reimports (the importer will not reset them when it regenerates the asset).

## Previewing in the editor

Opening a `SpineAsset` opens the Spine asset editor, which shows:

- A live viewport of the skeleton, driven by the same systems used at runtime.
- The animation list — click any animation to preview it (transitions honor `DefaultMix`).
- A scrubber timeline — pause and drag to scrub to an exact point in an animation.
- The bone hierarchy.
- The **Import scale** and **Default mix** controls, which update the preview live.

## Bone-follower sockets

To attach a prop, weapon, or effect to a moving bone (a "socket"), add a `SpineBoneFollowerComponent` to the follower entity. It requires a `GuidToIdTargetComponent` (added automatically), which is how you point at the skeleton entity from the editor — pick the target in the scene the same way as any other entity reference. Then set:

- **Bone Name** — the bone to follow, as authored in Spine.
- **Offset** — an additional pixel offset on top of the bone's world position.

Each frame, `SpineBoneFollowerSystem` (which runs after `SpineAnimationSystem`, so the pose is already resolved) moves the follower to the bone's world position. An unknown bone name logs an error and leaves the follower in place rather than throwing.

## What's supported

The integration currently covers importing, rendering, animation playback with crossfade, per-asset import scale, per-entity scale/flip, editor preview and scrubbing, the bone hierarchy view, and bone-follower sockets. Further authoring and runtime-control features — skins, a per-pair animation mix table, animation events routed into Murder's message system, per-slot tint, bounding-box hitboxes, and constraint control — are planned.

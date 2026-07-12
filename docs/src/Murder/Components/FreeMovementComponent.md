# FreeMovementComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FreeMovementComponent : IComponent
```

Temporarily disables solid/hole collision resolution for an entity in `SATPhysicsSystem`, letting it move through other colliders as if they were not there. This is runtime-only and never persisted or shown in the editor, since it represents a transient state (e.g. a cutscene move, a knockback, or a scripted teleport) rather than authored level data.

**Intent:** Give scripted or special-case movement (cutscenes, knockback, forced repositioning) a way to bypass normal solid-collision blocking for a short window, without having to change the entity's collider or collision mask.

**Use-case:** Add to an entity right before moving it somewhere that would otherwise be blocked by solids (e.g. through a wall during a scripted sequence), then remove it once the movement is complete; pass `FreeMovementFlags.RespectTiles` if the entity should still collide with tile-based level geometry while ignoring regular solid/hole colliders.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public FreeMovementComponent()
```

Enables free movement (ignoring solid/hole collisions) with no special flags.

```csharp
public FreeMovementComponent(FreeMovementFlags flags)
```

Enables free movement (ignoring solid/hole collisions) with the given `flags`.

**Parameters** \
`flags` [FreeMovementFlags](../../Murder/Components/FreeMovementFlags.html) \

### ⭐ Properties

#### Flags

```csharp
public readonly FreeMovementFlags Flags;
```

Flags controlling how collisions are ignored while this component is present. `DoNotClear` prevents the component from being automatically cleared, and `RespectTiles` forces tile-based collisions to still be respected even though solid/hole colliders are ignored.

**Returns** \
[FreeMovementFlags](../../Murder/Components/FreeMovementFlags.html) \

⚡

# EntityBoundsCacheComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct EntityBoundsCacheComponent : IComponent
```

Runtime-only cache of an entity's world-space bounding box.

**Intent:** `DynamicInCameraSystem` needs a bounding rectangle for every entity to decide whether to add/remove `InCameraComponent`. For entities with a `SpriteComponent` it can derive bounds from the sprite asset directly, but non-sprite entities (e.g. procedurally-shaped colliders or custom-drawn content) have no such asset to measure. This component lets those entities supply a precomputed `Bounds` rectangle instead, so the camera-visibility check has a cheap, ready-made value to compare against instead of recomputing bounds from scratch every frame.

**Use-case:** Add to non-sprite entities whose visible extent needs to participate in camera culling — set `Bounds` to the entity's world-space bounding rectangle so `DynamicInCameraSystem` can decide if it's currently on-screen.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public EntityBoundsCacheComponent(Rectangle bounds)
```

**Parameters** \
`bounds` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

### ⭐ Properties

#### Bounds

```csharp
public readonly Rectangle Bounds;
```

The entity's cached world-space bounding rectangle, compared against the camera's visible area.

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

⚡

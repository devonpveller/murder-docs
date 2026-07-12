# StaticComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct StaticComponent : IComponent
```

Marker component that flags an entity as non-moving, allowing physics and rendering systems to skip per-frame updates for it.

**Intent:** Signal that an entity will never change position so the engine can apply static-object optimisations instead of tracking it per frame.

**Use-case:** Attach to walls, floors, fixed props, or any entity whose position and shape will never change at runtime. `StaticRenderQuadTreeSystem` (filtering on `PositionComponent` + `SpriteComponent` + `StaticComponent`) inserts/removes such entities from a spatial quadtree once, instead of every frame, for efficient render culling; `DynamicInCameraSystem` explicitly excludes entities carrying `StaticComponent` from its per-frame "is this entity visible to the camera" recalculation, since a static entity's visibility only needs to be resolved via the quadtree. `TetheredComponent` also treats a `StaticComponent`-tagged side of a tether as an immovable anchor.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

⚡

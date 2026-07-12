# DynamicInCameraSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public sealed class DynamicInCameraSystem : IMonoPreRenderSystem, IRenderSystem, ISystem
```

Runs before the render pass to compute each dynamic (non-static) entity's bounding box and adds or removes `InCameraComponent` based on whether the entity falls within the camera viewport.

**Intent:** Performs per-frame camera culling for dynamic entities so that only visible sprites/colliders are processed by render and collision systems that filter on `InCameraComponent`. It tries the cheapest applicable check first: a sprite's AABB (accounting for parallax, scale and flip), a precomputed `EntityBoundsCacheComponent`, a collider's bounding box, or, failing all of those, a single-pixel point-in-camera test.

**Use-case:** Filters entities that have a `PositionComponent`, any of `SpriteComponent`/`AgentSpriteComponent`, and no `StaticComponent` — i.e. anything that moves and needs its in-camera status re-evaluated every frame. Static entities are expected to be culled once by a separate static-in-camera system instead, since their bounds never change.

**Implements:** _[IMonoPreRenderSystem](../../Murder/Core/Graphics/IMonoPreRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public DynamicInCameraSystem()
```

### ⭐ Methods

#### CalculateBounds(Vector2, Vector2, Point, Vector2, ImageFlip)

```csharp
public static Rectangle CalculateBounds(Vector2 position, Vector2 origin, Point size, Vector2 scale, ImageFlip flip = ImageFlip.None)
```

Returns a conservative axis-aligned bounding box that fully contains a sprite after scale, flip, origin offset and rotation, by computing a bounding circle around the sprite's half-extents and squaring it off. It is `static` and public so other systems (e.g. static camera culling or gizmo/debug drawing) can reuse the exact same conservative-bounds logic used for dynamic culling.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Point](../../Murder/Core/Geometry/Point.html) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`flip` [ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### BeforeDraw(Context)

```csharp
public void BeforeDraw(Context context)
```

For every matching entity, resolves the cheapest available bounds (sprite AABB with parallax applied, cached `EntityBoundsCacheComponent`, collider bounding box, or a 1-pixel fallback) and tests it against the camera's safe bounds (respecting any active `DisableSceneTransitionEffectsComponent.ForceCameraPosition` override), toggling `InCameraComponent` on the entity only when its visibility actually changes. Entities targeting the UI sprite batch are always treated as in-camera.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡

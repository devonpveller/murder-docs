# DynamicInCameraSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class DynamicInCameraSystem : IMonoPreRenderSystem, IRenderSystem, ISystem
```

Runs before the render pass to compute each dynamic (non-static) entity's bounding box and adds or removes `InCameraComponent` based on whether the entity falls within the camera viewport.

**Intent:** Performs per-frame camera culling for dynamic entities so that only visible sprites are processed by render systems.

**Use-case:** Required in any world with moving sprites; pair with the static camera system for complete camera-culling coverage.

**Implements:** _[IMonoPreRenderSystem](../../Murder/Core/Graphics/IMonoPreRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public DynamicInCameraSystem()
```

### ⭐ Methods
#### CalculateBounds(Vector2, Vector2, Point, Vector2)
```csharp
public Rectangle CalculateBounds(Vector2 position, Vector2 origin, Point size, Vector2 scale)
```

Returns a conservative axis-aligned bounding box that fully contains the sprite after scale, flip, and origin offset; used internally to determine whether a sprite is visible to the camera.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Point](../../Murder/Core/Geometry/Point.html) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### BeforeDraw(Context)
```csharp
public virtual void BeforeDraw(Context context)
```

Iterates all dynamic entities and adds or removes `InCameraComponent` based on whether their computed bounding box overlaps the current camera viewport.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡
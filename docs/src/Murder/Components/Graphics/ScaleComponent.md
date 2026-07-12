# ScaleComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct ScaleComponent : IComponent
```

Overrides the rendering scale of an entity's sprite on both axes independently.

**Intent:** Stretch, shrink, or mirror a sprite at render time without modifying the underlying asset. Both `SpriteRenderSystem` and `AgentSpriteSystem` read `Scale` (defaulting to `Vector2.One` when the component is absent) and pass it straight through to `RenderServices.DrawSprite`/`RenderServices.DrawAsepriteAnimationFrame`, so it affects only the draw call — an entity's collider, position, and other gameplay bounds are unaffected. `DynamicInCameraSystem` also factors it into the on-screen bounding box used for culling, so a scaled-up sprite is correctly kept "in camera" even if its unscaled bounds would otherwise be off-screen.

**Use-case:** Attach to an entity and provide the desired `Scale` vector (e.g. `new Vector2(2, 2)` to double the sprite's rendered size, or a negative component to mirror it) — the render systems multiply the sprite dimensions by these values before drawing. Useful for squash/stretch effects, one-off size variations, or animating a "grow/shrink" tween by replacing the component each frame.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public ScaleComponent(float scaleX, float scaleY)
```

**Parameters** \
`scaleX` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`scaleY` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public ScaleComponent(Vector2 scale)
```

**Parameters** \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### Scale

```csharp
public readonly Vector2 Scale;
```

Scale multiplier applied to the sprite on the X and Y axes (1, 1 = original size).

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

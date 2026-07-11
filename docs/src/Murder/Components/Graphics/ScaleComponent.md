# ScaleComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct ScaleComponent : IComponent
```

Overrides the rendering scale of an entity's sprite on both axes independently.

**Intent:** Stretch, shrink, or mirror a sprite at render time without modifying the underlying asset.

**Use-case:** Attach to an entity and provide the desired `Scale` vector; the render system multiplies the sprite dimensions by these values before drawing.

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
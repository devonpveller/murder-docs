# IMurderTransformComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public abstract IMurderTransformComponent : ITransformComponent, IParentRelativeComponent, IComponent
```

This is an interface for transform components within the game.

**Intent:** Provide a common contract for all transform components in Murder so that systems can read and manipulate position, rotation, and scale without depending on a concrete type.

**Use-case:** Use this interface in systems and services that operate on any positionable entity; call `GetMurderTransform()` (via `MurderTransformExtensions`) on an entity to retrieve its concrete transform regardless of the implementing type.

**Implements:** _[ITransformComponent](../../Bang/Components/ITransformComponent.html), [IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Properties
#### Angle
```csharp
public abstract virtual float Angle { get; }
```

Rotation angle (in radians) of this transform component.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Cx
```csharp
public virtual int Cx { get; }
```

This is the X grid coordinate. See [GridConfiguration](../../Murder/Core/GridConfiguration.html) for more details on our grid specs.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Cy
```csharp
public virtual int Cy { get; }
```

This is the Y grid coordinate. See [GridConfiguration](../../Murder/Core/GridConfiguration.html) for more details on our grid specs.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Point
```csharp
public virtual Point Point { get; }
```

Position expressed as an integer grid `Point`, snapped to the nearest grid cell.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
#### Scale
```csharp
public abstract virtual Vector2 Scale { get; }
```

Scale of this transform on X and Y axes.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Vector2
```csharp
public virtual Vector2 Vector2 { get; }
```

Position expressed as a floating-point `Vector2`.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### X
```csharp
public abstract virtual float X { get; }
```

Relative X position of the component.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Y
```csharp
public abstract virtual float Y { get; }
```

Relative Y position of the component.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### Add(IMurderTransformComponent)
```csharp
public abstract IMurderTransformComponent Add(IMurderTransformComponent r)
```

Returns a new transform that is the sum of this transform and `r`.

**Parameters** \
`r` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### Add(Vector2)
```csharp
public abstract IMurderTransformComponent Add(Vector2 r)
```

Returns a new transform offset by the given `Vector2`.

**Parameters** \
`r` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### GetGlobal()
```csharp
public abstract IMurderTransformComponent GetGlobal()
```

Returns the world-space (global) version of this transform, resolving any parent-relative offsets.

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### Subtract(IMurderTransformComponent)
```csharp
public abstract IMurderTransformComponent Subtract(IMurderTransformComponent r)
```

Returns a new transform that is the difference of this transform and `r`.

**Parameters** \
`r` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### Subtract(Vector2)
```csharp
public abstract IMurderTransformComponent Subtract(Vector2 r)
```

Returns a new transform with the given `Vector2` subtracted from its position.

**Parameters** \
`r` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### With(float, float)
```csharp
public abstract IMurderTransformComponent With(float x, float y)
```

Returns a new transform with `X` and `Y` replaced by the given values, preserving other fields.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### Add(Point)
```csharp
public virtual IMurderTransformComponent Add(Point r)
```

Returns a new transform offset by the given grid `Point`.

**Parameters** \
`r` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### Subtract(Point)
```csharp
public virtual IMurderTransformComponent Subtract(Point r)
```

Returns a new transform with the given grid `Point` subtracted from its position.

**Parameters** \
`r` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### With(Point)
```csharp
public virtual IMurderTransformComponent With(Point p)
```

Returns a new transform with position set to the given grid `Point`.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### With(Vector2)
```csharp
public virtual IMurderTransformComponent With(Vector2 p)
```

Returns a new transform with position set to the given `Vector2`.

**Parameters** \
`p` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \



⚡
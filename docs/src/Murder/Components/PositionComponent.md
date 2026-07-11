# PositionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PositionComponent : IMurderTransformComponent, ITransformComponent, IParentRelativeComponent, IComponent, IEquatable<T>
```

Position component used to track entities positions within a grid.

**Intent:** Store the 2D world-space position (X, Y) of an entity, optionally relative to a parent transform.

**Use-case:** Attach to every entity that occupies a position in the game world; systems that move, render, or collide entities all read or write this component.

**Implements:** _[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html), [ITransformComponent](../../Bang/Components/ITransformComponent.html), [IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html), [IComponent](../../Bang/Components/IComponent.html), [IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors
```csharp
public PositionComponent(Point p)
```

Create a new [PositionComponent](../../Murder/Components/PositionComponent.html).

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
\

```csharp
public PositionComponent(float x, float y, IMurderTransformComponent parent)
```

Create a new [PositionComponent](../../Murder/Components/PositionComponent.html) with an explicit parent transform.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`parent` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

```csharp
public PositionComponent(float x, float y)
```

Create a new [PositionComponent](../../Murder/Components/PositionComponent.html).

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public PositionComponent(Vector2 v)
```

Create a new [PositionComponent](../../Murder/Components/PositionComponent.html).

**Parameters** \
`v` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\

### ⭐ Properties
#### Angle
```csharp
public virtual float Angle { get; }
```

Rotation angle of the transform, in radians. Always 0 for a plain position component.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### HasParent
```csharp
public virtual bool HasParent { get; }
```

Whether this position is tracking a parent entity.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Scale
```csharp
public virtual Vector2 Scale { get; }
```

Scale of the transform. Always (1, 1) for a plain position component.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### X
```csharp
public virtual float X { get; }
```

Relative X position of the component.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Y
```csharp
public virtual float Y { get; }
```

Relative Y position of the component.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### Equals(PositionComponent)
```csharp
public virtual bool Equals(PositionComponent other)
```

Compares two position components. This will take their parents into account.

**Parameters** \
`other` [PositionComponent](../../Murder/Components/PositionComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Object)
```csharp
public virtual bool Equals(Object obj)
```

Checks equality with an arbitrary object.

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Add(IMurderTransformComponent)
```csharp
public virtual IMurderTransformComponent Add(IMurderTransformComponent r)
```

Returns a new transform that is the sum of this position and `r`.

**Parameters** \
`r` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### Add(Vector2)
```csharp
public virtual IMurderTransformComponent Add(Vector2 r)
```

Returns a new transform offset by the given vector.

**Parameters** \
`r` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### GetGlobal()
```csharp
public virtual IMurderTransformComponent GetGlobal()
```

Return the global position of the component within the world.

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### Subtract(IMurderTransformComponent)
```csharp
public virtual IMurderTransformComponent Subtract(IMurderTransformComponent r)
```

Returns a new transform that is the difference between this position and `r`.

**Parameters** \
`r` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### Subtract(Vector2)
```csharp
public virtual IMurderTransformComponent Subtract(Vector2 r)
```

Returns a new transform with the given vector subtracted from this position.

**Parameters** \
`r` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### With(float, float)
```csharp
public virtual IMurderTransformComponent With(float x, float y)
```

Returns a new transform at the specified absolute X and Y coordinates.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### GetHashCode()
```csharp
public virtual int GetHashCode()
```

Returns a hash code based on X and Y coordinates.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### WithoutParent()
```csharp
public virtual IParentRelativeComponent WithoutParent()
```

Creates a copy of component with the relative coordinates without its parent.

**Returns** \
[IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html) \
\

#### OnParentModified(IComponent, Entity)
```csharp
public virtual void OnParentModified(IComponent parentComponent, Entity childEntity)
```

This tracks whenever a parent position has been modified.

**Parameters** \
`parentComponent` [IComponent](../../Bang/Components/IComponent.html) \
\
`childEntity` [Entity](../../Bang/Entities/Entity.html) \
\



⚡
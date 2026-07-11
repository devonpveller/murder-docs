# PositionComponent

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public readonly struct PositionComponent : IParentRelativeComponent, IEquatable<PositionComponent>
```

Position component used to track entities positions.

`PositionComponent` is the built-in, foundational component for where an entity is in the world.
It is deliberately minimal — just a relative `X`/`Y` pair plus an optional cached global position
— and is the component nearly every visible or simulated entity in a Murder/Bang game will carry.
It is decorated with [IntrinsicAttribute](../../Bang/Attributes/IntrinsicAttribute.html), meaning
an entity made up of only a `PositionComponent` (and other intrinsic components) is not considered
distinct enough to be worth serializing on its own — having a position alone doesn't make an
entity meaningful game data.

The component implements [IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html),
which is what makes entity hierarchies (parenting) work for position: `X`/`Y` are always the
position *relative to the parent* (or relative to the world origin if there is no parent), while
`GetGlobal()` resolves the actual world-space position, using a cached `_globalPosition` when the
component is tracking a parent, or falling back to `(X, Y)` otherwise. Whenever a parent entity's
own `PositionComponent` changes, the engine calls `OnParentModified` on each child's
`PositionComponent`, which adds the parent's resolved global position to the child's local offset
and writes the result back via `Entity.ReplaceComponent`. Because `PositionComponent` is a
`readonly struct`, "moving" an entity always means constructing a new `PositionComponent` (via one
of the constructors, `WithLocal`, arithmetic operators, or `SetGlobal`) and replacing the old one —
there is no way to mutate X/Y in place. Systems that read or write entity position (movement,
physics, rendering, camera, pathfinding, etc.) all do so through this component, typically via
`Entity.GetPosition()`/`Entity.SetPosition(...)` extension helpers built on top of it.

**Implements:** _[IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html), [IEquatable\<PositionComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors
```csharp
public PositionComponent(float x, float y)
```

Create a new [PositionComponent](../../Bang/Components/PositionComponent.html) with no parent
(the global position is left unset and, when queried via `GetGlobal()`, will simply be `(x, y)`).
This is the constructor used by JSON deserialization (`[JsonConstructor]`).

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

```csharp
public PositionComponent(float x, float y, Vector2? globalPosition)
```

Create a new [PositionComponent](../../Bang/Components/PositionComponent.html), optionally caching
a pre-computed global (world-space) position. This overload is used internally when a parent
notifies this component of its resolved global position via `OnParentModified`, so the global
value does not need to be recomputed by walking the parent chain on every read.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`globalPosition` [Vector2?](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\

```csharp
public PositionComponent(Vector2 v)
```

Create a new [PositionComponent](../../Bang/Components/PositionComponent.html) from a `Vector2`
coordinate, with no parent.

**Parameters** \
`v` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\

```csharp
public PositionComponent(Point p)
```

Create a new [PositionComponent](../../Bang/Components/PositionComponent.html) from an integer
`Point` coordinate, with no parent.

**Parameters** \
`p` [Point](https://learn.microsoft.com/en-us/dotnet/api/System.Drawing.Point?view=net-7.0) \
\

### ⭐ Properties
#### X
```csharp
public float X { get; }
```

Relative X position of the component.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Y
```csharp
public float Y { get; }
```

Relative Y position of the component.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Angle
```csharp
public float Angle { get; }
```

Rotation angle of this component. A plain `PositionComponent` only tracks position, so this
always returns zero; it exists to satisfy consumers that expect a transform-like shape.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Scale
```csharp
public Vector2 Scale { get; }
```

Scale of this component. A plain `PositionComponent` does not track scale, so this always
returns `Vector2.One`.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Vector2
```csharp
public Vector2 Vector2 { get; }
```

The relative (local) `X`/`Y` position as a `Vector2`. This does not include the parent offset;
use `GetGlobal()` for the world-space value.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### HasParent
```csharp
public bool HasParent { get; }
```

Whether this position is tracking a parent entity (i.e. whether a cached global position has
been set).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Methods
#### GetGlobal()
```csharp
public Vector2 GetGlobal()
```

Return the global position of the component within the world. If this component is tracking a
parent, returns the cached global position; otherwise returns `(X, Y)` directly.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SetGlobal(Vector2)
```csharp
public PositionComponent SetGlobal(Vector2 position)
```

Return a copy of the component with its global (world-space) position set to `position`. If this
component is already tracking a parent, the local `X`/`Y` are recomputed so the entity ends up at
the requested global position while remaining relative to the same parent offset; otherwise the
new component simply has `position` as both its local and global coordinates.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### WithLocal(Vector2)
```csharp
public PositionComponent WithLocal(Vector2 localPosition)
```

Creates a copy of this component with its local coordinates set to `localPosition`, preserving
its relationship to any tracked parent (the global position is shifted accordingly).

**Parameters** \
`localPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### WithLocal(float, float)
```csharp
public PositionComponent WithLocal(float x, float y)
```

Creates a copy of this component with its local coordinates set to `(x, y)`. If this component is
tracking a parent, the cached global position is adjusted by the same delta so the entity keeps
following its parent correctly; otherwise this behaves like a plain constructor call.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### WithoutParent()
```csharp
public IParentRelativeComponent WithoutParent()
```

Creates a copy of the component with the relative coordinates without its parent — the cached
global position is discarded and only the local `X`/`Y` are kept.

**Returns** \
[IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html) \

#### OnParentModified(IComponent, Entity)
```csharp
public void OnParentModified(IComponent parentComponent, Entity childEntity)
```

This tracks whenever a parent position has been modified. Adds the parent's resolved global
position to this component's local `X`/`Y` and replaces `childEntity`'s `PositionComponent` with
the combined global position via `Entity.ReplaceComponent`.

**Parameters** \
`parentComponent` [IComponent](../../Bang/Components/IComponent.html) \
\
`childEntity` [Entity](../../Bang/Entities/Entity.html) \
\

#### GetHashCode()
```csharp
public override int GetHashCode()
```

Computes a hash code based on the local `X`/`Y` coordinates only (the cached global position, if
any, does not participate in the hash).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Equals(PositionComponent)
```csharp
public bool Equals(PositionComponent other)
```

Compares two position components. This will take their parents into account: two components with
the same local `X`/`Y` are only equal if they also agree on whether (and to what) they are
parented, so a parented and an unparented component with identical local coordinates are not
equal.

**Parameters** \
`other` [PositionComponent](../../Bang/Components/PositionComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Object)
```csharp
public override bool Equals(Object obj)
```

Checks equality with an arbitrary object, delegating to `Equals(PositionComponent)` when `obj` is
also a `PositionComponent`.

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### operator ==(PositionComponent, PositionComponent)
```csharp
public static bool operator ==(PositionComponent l, PositionComponent r)
```

Compares two components by value, see `Equals(PositionComponent)`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### operator !=(PositionComponent, PositionComponent)
```csharp
public static bool operator !=(PositionComponent l, PositionComponent r)
```

Compares two components by value, see `Equals(PositionComponent)`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### operator +(PositionComponent, PositionComponent)
```csharp
public static PositionComponent operator +(PositionComponent l, PositionComponent r)
```

Adds the relative `X`/`Y` of both components. Note this only combines the local coordinates and
discards any cached global position from either operand.

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### operator -(PositionComponent, PositionComponent)
```csharp
public static PositionComponent operator -(PositionComponent l, PositionComponent r)
```

Subtracts the relative `X`/`Y` of both components. Note this only combines the local coordinates
and discards any cached global position from either operand.

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### operator +(PositionComponent, Vector2)
```csharp
public static PositionComponent operator +(PositionComponent l, Vector2 r)
```

Offsets the relative `X`/`Y` of the component by a `Vector2`, discarding any cached global
position.

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### operator -(PositionComponent, Vector2)
```csharp
public static PositionComponent operator -(PositionComponent l, Vector2 r)
```

Offsets the relative `X`/`Y` of the component by a `Vector2`, discarding any cached global
position.

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \



⚡
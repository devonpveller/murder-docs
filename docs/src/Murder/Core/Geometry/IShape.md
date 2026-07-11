# IShape

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public abstract IShape
```

An IShape is a component which will be applied physics properties for collision.

**Intent:** Define the contract for all collision shapes used by `ColliderComponent`.

**Use-case:** Implement `IShape` when creating a custom collision shape. Use `GetBoundingBox()` for broad-phase culling and `GetPolygon()` for precise SAT-based overlap tests.

### ⭐ Methods
#### GetPolygon()
```csharp
public abstract PolygonShape GetPolygon()
```

Returns a polygon approximation of this shape, used for SAT collision detection.

**Returns** \
[PolygonShape](../../../Murder/Core/Geometry/PolygonShape.html) \

#### GetBoundingBox()
```csharp
public abstract Rectangle GetBoundingBox()
```

Returns the axis-aligned bounding box of this shape, used for broad-phase collision culling.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \



⚡
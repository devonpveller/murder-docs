# IShape

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public abstract IShape
```

Common contract for every collision shape (`BoxShape`, `CircleShape`, `LineShape`, `PointShape`, `PolygonShape`, `LazyShape`) that can be attached to a `ColliderComponent`.

**Intent:** Define the contract for all collision shapes used by `ColliderComponent`, so physics/collision code can operate uniformly over a mix of different shape kinds stored together as `ImmutableArray<IShape>`.

**Use-case:** Implement `IShape` when creating a custom collision shape. Use `GetBoundingBox()` for broad-phase culling and `GetPolygon()` for precise SAT-based overlap tests.

### ⭐ Methods

#### GetPolygon()

```csharp
public abstract PolygonShape GetPolygon()
```

Returns a `PolygonShape` approximation of this shape, used for precise SAT (Separating Axis Theorem) collision detection and for debug/editor rendering of the shape's outline.

**Returns** \
[PolygonShape](../../../Murder/Core/Geometry/PolygonShape.html) \

#### GetBoundingBox()

```csharp
public abstract Rectangle GetBoundingBox()
```

Returns the axis-aligned bounding box of this shape, in local space. Used for cheap broad-phase collision culling before running a more expensive exact test via `GetPolygon()`.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

⚡

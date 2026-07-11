# ColliderServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class ColliderServices
```

Helpers for computing bounding boxes, grid snapping, and center points from entity colliders.

**Intent:** Provides geometry utilities that operate directly on entities with `ColliderComponent` and `PositionComponent`.

**Use-case:** Use to determine where an entity sits in world or grid space without manually querying its components, such as when placing objects on a tile grid or centering a HUD element over an entity.

### ⭐ Methods
#### GetBoundingBox(Entity)
```csharp
public IntRectangle GetBoundingBox(Entity e)
```
Returns the integer bounding rectangle of the entity's collider in world coordinates.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### ToGrid(IntRectangle)
```csharp
public IntRectangle ToGrid(IntRectangle rectangle)
```
Converts a pixel-space rectangle to grid-cell coordinates by dividing by `Grid.CellSize`.

**Parameters** \
`rectangle` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetCollidersBoundingBox(Entity, bool)
```csharp
public IntRectangle[] GetCollidersBoundingBox(Entity e, bool gridCoordinates)
```
Returns per-shape bounding boxes for all shapes in the entity's collider, optionally in grid space.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`gridCoordinates` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[IntRectangle[]](../../Murder/Core/Geometry/IntRectangle.html) \

#### FindCenter(Entity)
```csharp
public Point FindCenter(Entity e)
```

Returns the center point of an entity with all its colliders.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### GetCenterOf(Entity)
```csharp
public Vector2 GetCenterOf(Entity e)
```
Returns the world-space center point of the entity, accounting for its collider offset and size.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SnapToGrid(Vector2)
```csharp
public Vector2 SnapToGrid(Vector2 positive)
```
Snaps a world-space position to the nearest grid cell origin.

**Parameters** \
`positive` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SnapToRelativeGrid(Vector2, Vector2)
```csharp
public Vector2 SnapToRelativeGrid(Vector2 position, Vector2 origin)
```
Snaps a position to the nearest grid cell relative to a given origin point.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \



⚡
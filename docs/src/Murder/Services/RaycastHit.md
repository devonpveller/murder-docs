# RaycastHit

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
sealed struct RaycastHit
```

Holds the result of a `PhysicsServices.Raycast` or `RaycastTiles` call, identifying what was hit and at what world position.

**Intent:** Returns collision information from a ray query in a single, lightweight value type.

**Use-case:** Check `Entity` to identify which entity the ray struck (or `Tile` for tile hits), then use `Point` to determine the exact world position of the intersection for effects or spawning.

### ⭐ Constructors
```csharp
public RaycastHit()
```
Creates an empty `RaycastHit` with no entity, no tile, and `Point` at the origin.

```csharp
public RaycastHit(Entity entity, Vector2 point)
```
Creates a `RaycastHit` recording an entity collision at `point`.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public RaycastHit(Point tile, Vector2 point)
```
Creates a `RaycastHit` recording a tile collision at the grid cell `tile` and the world-space intersection `point`.

**Parameters** \
`tile` [Point](../../Murder/Core/Geometry/Point.html) \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties
#### Entity
```csharp
public readonly Entity Entity;
```
The entity that was struck by the ray, or `null` if the hit was against a tile.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
#### Point
```csharp
public readonly Vector2 Point;
```
The world-space position at which the ray intersected the collider or tile surface.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Tile
```csharp
public readonly Point Tile;
```
The grid-space coordinates of the tile that was struck, or the default value if the hit was against an entity.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \


⚡
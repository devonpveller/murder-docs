# RaycastHit

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public sealed struct RaycastHit
```

Result of a `PhysicsServices.Raycast` or `PhysicsServices.RaycastTiles` call (declared as a nested type, `PhysicsServices.RaycastHit`), identifying what was hit and at what world position.

**Intent:** Carries collision information from a ray query in a single, lightweight value type — either an `Entity` hit, a `Tile` hit, or (when the query returned `false`) a default/empty value with neither set.

**Use-case:** Check `Entity` (non-null) to identify which entity the ray struck, or `Tile` when the ray hit map geometry instead — a given `RaycastHit` is only ever meaningfully populated with one of the two, based on which raycast method produced it. Use `Point` to determine the exact world position of the intersection for spawning impact effects, stopping a projectile, or drawing a debug line.

### ⭐ Constructors

```csharp
public RaycastHit()
```

Creates an empty `RaycastHit` with no entity, no tile, and `Point` at `Vector2.Zero`. This is the value `PhysicsServices.Raycast`/`RaycastTiles` produce (via `out RaycastHit hit`, implicitly defaulted) when the ray does not hit anything.

```csharp
public RaycastHit(Point tile, Vector2 point)
```

Creates a `RaycastHit` recording a tile collision at the grid cell `tile` and the world-space intersection `point`. Produced internally by `PhysicsServices.RaycastTiles` when the ray crosses a flagged tile.

**Parameters** \
`tile` [Point](../../Murder/Core/Geometry/Point.html) \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public RaycastHit(Entity? entity, Vector2 point)
```

Creates a `RaycastHit` recording an entity collision at `point`. Produced internally by `PhysicsServices.Raycast` when the ray intersects an entity's collider shape.

**Parameters** \
`entity` [Entity?](../../Bang/Entities/Entity.html) \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### Entity

```csharp
public Entity? Entity { get; }
```

The entity that was struck by the ray, or `null` if the hit was against a tile (or if there was no hit at all).

**Returns** \
[Entity?](../../Bang/Entities/Entity.html) \

#### Point

```csharp
public Vector2 Point { get; }
```

The world-space position at which the ray intersected the collider or tile surface (`Vector2.Zero` if there was no hit).

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Tile

```csharp
public Point Tile { get; }
```

The grid-space coordinates of the tile that was struck, or the default value (`Point.Zero`) if the hit was against an entity (or if there was no hit at all).

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

⚡

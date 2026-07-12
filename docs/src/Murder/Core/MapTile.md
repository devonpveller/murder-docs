# MapTile

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public struct MapTile
```

Per-cell payload stored inside a `Map`, holding the collision bitmask and pathfinding weight for a single tile.

**Intent:** Lightweight value type that bundles everything the engine needs to know about a single grid cell at runtime (collision layers and traversal weight) into one struct, so both can be read or written together instead of via separate parallel arrays.

**Use-case:** Read via `Map.GetGridMap` to inspect both the collision and weight data for a specific tile at once; the individual fields are otherwise mutated internally by `Map`'s collision/carve methods (`SetOccupied`, `SetOccupiedAsCarve`, `SetOccupiedAsStatic`, etc.) as map-building systems and carve entities populate the map.

### ⭐ Constructors

```csharp
public MapTile()
```

Creates a default tile with no collision and a traversal weight of 1.

```csharp
public MapTile(int weight)
```

Creates a tile with no collision and the specified pathfinding traversal `weight`.

**Parameters** \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### CollisionType

```csharp
public int CollisionType;
```

Bitmask of collision layers active on this tile (see `CollisionLayersBase` constants).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Weight

```csharp
public int Weight;
```

Pathfinding traversal cost for this tile; higher values make it less desirable for pathfinding routes.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

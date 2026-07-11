# MapTile

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct MapTile
```

Per-cell data stored inside a `Map`, holding the collision bitmask and pathfinding weight for a single tile.

**Intent:** Lightweight value type that encodes everything the engine needs to know about a single grid cell at runtime.

**Use-case:** Read via `Map.GetGridMap` to inspect collision or weight data for a specific tile; written by map-building systems when populating the map from tilemap assets.

### ⭐ Constructors
```csharp
public MapTile()
```

Creates a default tile with no collision and zero weight.

```csharp
public MapTile(int weight)
```

Creates a tile with the specified pathfinding traversal weight and no collision.

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
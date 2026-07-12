# TilesetGridType

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class TilesetGridType
```

Integer constants for the two fundamental tileset grid cell types: empty space and solid collision.

**Intent:** Provide named constants for a simple two-state (empty/solid) classification of a tileset cell.

**Use-case:** These constants are **not** currently wired into the engine's actual tile/grid collision system — `Map`/`MapTile` (see [Map](../../../Murder/Core/Map.html)) represent per-cell collision as a `CollisionLayersBase` bitmask, and no code under `src/Murder` or `src/Murder.Editor` reads or writes `TilesetGridType.Empty`/`TilesetGridType.Solid`. Treat this type as a lightweight, standalone pair of constants you can use in your own game code (e.g. a custom minimap or tile-authoring tool that only needs a boolean "is this cell blocked" concept) rather than as the value the engine stores for tile collision.

### ⭐ Constructors

```csharp
public TilesetGridType()
```

### ⭐ Properties

#### Empty

```csharp
public static const int Empty;
```

Cell type value representing an open, passable tile (value: 0).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Solid

```csharp
public static const int Solid;
```

Cell type value representing a solid, impassable tile (value: 1).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

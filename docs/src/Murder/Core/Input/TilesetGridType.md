# TilesetGridType

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class TilesetGridType
```

Integer constants for the two fundamental tileset grid cell types: empty space and solid collision.

**Intent:** Provide named constants for tileset cell type classification.

**Use-case:** Compare a cell value against `TilesetGridType.Solid` or `TilesetGridType.Empty` when querying the tile grid to determine whether a cell blocks movement.

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
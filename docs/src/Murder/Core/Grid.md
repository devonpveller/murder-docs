# Grid

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public static class Grid
```

Helper static class that forwards the values of the default [Game.Grid](../../Murder/Game.html#grid) for easier access.

**Intent:** Provides convenient static shortcuts to the active `GridConfiguration` so code doesn't need to reference `Game.Grid` directly.

**Use-case:** Use these static members anywhere you need the current cell size or need to snap a world-space float to the nearest grid cell.

### ⭐ Properties
#### CellDimensions
```csharp
public static Point CellDimensions { get; }
```

The grid cell size as a `Point` (same value on both axes).

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
#### CellSize
```csharp
public static int CellSize { get; }
```

The width and height of a single grid cell in world-space pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### HalfCellDimensions
```csharp
public static Point HalfCellDimensions { get; }
```

Half the cell dimensions as a `Point`, useful for centering within a cell.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
#### HalfCellSize
```csharp
public static int HalfCellSize { get; }
```

Half of `CellSize`, i.e. the distance from the center of a cell to its edge.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### CeilToGrid(float)
```csharp
public int CeilToGrid(float value)
```

Converts a world-space float to the grid cell index it falls in, rounding up.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### FloorToGrid(float)
```csharp
public int FloorToGrid(float value)
```

Converts a world-space float to the grid cell index it falls in, rounding down.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RoundToGrid(float)
```csharp
public int RoundToGrid(float value)
```

Converts a world-space float to the nearest grid cell index using standard rounding.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
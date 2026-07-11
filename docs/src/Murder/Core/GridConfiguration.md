# GridConfiguration

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct GridConfiguration
```

Defines the dimensions of the game's tile grid, including cell size and derived half-size values.

**Intent:** Central configuration for the tile grid that drives world-to-grid coordinate conversions.

**Use-case:** Set once via `Game.Grid` at startup; all coordinate helpers read from this configuration when snapping world positions to tile cells.

### ⭐ Constructors
```csharp
public GridConfiguration(int cellSize)
```

Default constructor

**Parameters** \
`cellSize` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

### ⭐ Properties
#### CellDimensions
```csharp
public readonly Point CellDimensions;
```

A point that is [GridConfiguration.CellSize](../../Murder/Core/GridConfiguration.html#cellsize).

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
#### CellSize
```csharp
public readonly int CellSize;
```

Size of this grid's individual cell.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### HalfCellDimensions
```csharp
public readonly Point HalfCellDimensions;
```

A point that is [GridConfiguration.HalfCellSize](../../Murder/Core/GridConfiguration.html#halfcellsize).

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
#### HalfCellSize
```csharp
public readonly int HalfCellSize;
```

[GridConfiguration.CellSize](../../Murder/Core/GridConfiguration.html#cellsize) divided by two.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### CeilToGrid(float)
```csharp
public int CeilToGrid(float value)
```

Find in which cell of the grid a value would land, rounding up.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

#### FloorToGrid(float)
```csharp
public int FloorToGrid(float value)
```

Find in which cell of the grid a value would land, rounding down.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

#### RoundToGrid(float)
```csharp
public int RoundToGrid(float value)
```

Find in which cell of the grid a value would land, with default [Calculator.RoundToInt(System.Single)](../../Murder/Utilities/Calculator.html#roundtoint(float) behavior.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\



⚡
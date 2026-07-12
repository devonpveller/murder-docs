# GridConfiguration

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct GridConfiguration
```

Defines the dimensions of the game's tile grid, including cell size and derived half-size values.

**Intent:** Central configuration for the tile grid that drives world-to-grid coordinate conversions. A single instance of this is held by `Game.Grid` and represents the one cell size used throughout a game's tile-based systems (map collision, pathfinding, tile rendering, etc.).

**Use-case:** Set once via `Game.Grid` at startup (typically derived from `GameProfile`); all coordinate helpers, including the static `Grid` class, read from this configuration when snapping world positions to tile cells or converting a cell size into pixel dimensions.

### ⭐ Constructors

```csharp
public GridConfiguration(int cellSize)
```

Creates a grid configuration from a single `cellSize`, deriving `HalfCellSize`, `CellDimensions`, and `HalfCellDimensions` from it.

**Parameters** \
`cellSize` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### CellDimensions

```csharp
public readonly Point CellDimensions;
```

A point that is `CellSize` by `CellSize`.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### CellSize

```csharp
public readonly int CellSize;
```

Size of this grid's individual cell, in world-space pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### HalfCellDimensions

```csharp
public readonly Point HalfCellDimensions;
```

A point that is `HalfCellSize` by `HalfCellSize`.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### HalfCellSize

```csharp
public readonly int HalfCellSize;
```

`CellSize` divided by two, rounded to the nearest integer.

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

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### FloorToGrid(float)

```csharp
public int FloorToGrid(float value)
```

Find in which cell of the grid a value would land, rounding down.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RoundToGrid(float)

```csharp
public int RoundToGrid(float value)
```

Find in which cell of the grid a value would land, with default `Calculator.RoundToInt(float)` rounding behavior.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

# TileGrid

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class TileGrid
```

Stores a single tilemap layer's worth of tile data as a flat, resizable 2D array of integer bitmasks, plus a cache of the auto-tiled sprite/occlusion info derived from it.

**Intent:** The data layer for tilemap rendering. `TileGridComponent`/`RoomComponent` hold a `TileGrid`; systems like `TilemapAndFloorRenderSystem`/`FloorWithBatchOptimizationRenderSystem` read from it via `GetTile` to know which auto-tiled sprite slice to draw at each cell, and `TileServices`/the map editor mutate it via `Set`/`Unset` and friends.

**Use-case:** Unlike `Map` (which stores the world's actual collision bitmask), `TileGrid` is purely a per-layer, per-room authoring/rendering grid — each cell's `int` value is an arbitrary bitmask meaningful to whatever tileset is drawing it. Use `Set`/`Unset`/`SetGridPosition`/`UnsetGridPosition` to paint or erase tiles, `At`/`AtGridPosition`/`HasFlagAt` to query them, and `GetTile` from a render system to fetch the auto-tiled sprite slice for a cell.

### ⭐ Constructors

```csharp
public TileGrid(Point origin, int width, int height)
```

Creates an empty tile grid of the given size at the given world-space origin. All cells start at `0` (no bits set).

**Parameters** \
`origin` [Point](../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Height

```csharp
public int Height { get; }
```

The height of this tile grid, in tile units.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Origin

```csharp
public Point Origin { get; }
```

The world-space grid coordinate of this grid's top-left cell (cell `(0, 0)` in local space).

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Width

```csharp
public int Width { get; }
```

The width of this tile grid, in tile units.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### HasFlagAtGridPosition(int, int, int)

```csharp
public bool HasFlagAtGridPosition(int x, int y, int value)
```

Checks whether is solid at a position `x` and `y`.
This will take a position from the grid (world) back to the local grid, using [TileGrid.Origin](../../Murder/Core/TileGrid.html#origin).

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### At(Point)

```csharp
public int At(Point p)
```

Returns the raw tile bitmask stored at local grid position `p`, or `0` if out of bounds.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### At(int, int)

```csharp
public int At(int x, int y)
```

Returns the raw tile bitmask stored at local grid coordinates `x`, `y`, or `0` if out of bounds.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AtGridPosition(Point)

```csharp
public int AtGridPosition(Point p)
```

Returns the raw tile bitmask at the given world-space grid position, converting it to a local coordinate by subtracting `Origin` first.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetTile(ImmutableArray\<Entity\>, int, int, int, int)

```csharp
public (int tile, int sortAdjust, bool occludeGround) GetTile(ImmutableArray<Entity> tileEntities, int index, int totalTilemaps, int x, int y)
```

Returns the auto-tiled sprite information for the tilemap layer at index `index` (out of `totalTilemaps` total layers), at local grid coordinates `x`, `y`. Rebuilds the internal auto-tile cache first if the number of cached layers doesn't match `totalTilemaps` (e.g. after tiles were added/removed via `Set`/`Unset`). Used by tilemap render systems to pick which auto-tile sprite slice and draw-order adjustment to use for each cell, and whether that cell occludes the floor beneath it.

**Parameters** \
`tileEntities` [ImmutableArray\<Entity\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`totalTilemaps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[ValueTuple\<int, int, bool\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-3?view=net-7.0). Returns `(-1, 0, false)` when out of bounds. \

#### HasFlagAt(int, int, int)

```csharp
public virtual bool HasFlagAt(int x, int y, int value)
```

Checks whether the tile bitmask at local coordinates `x`, `y` has every bit of `value` set. Virtual so derived grid types (e.g. ones backed by a different storage scheme) can override the lookup while keeping the rest of `TileGrid`'s API working against them.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### MoveFromTo(Point, Point, Point)

```csharp
public void MoveFromTo(Point from, Point to, Point size)
```

Moves a rectangular block of tile values from one location to another within the grid: reads each cell in the `size`-sized block starting at `from`, clears it, and writes the same value at the corresponding offset starting at `to`. Used by the editor when the user drags a selection of tiles to a new position.

**Parameters** \
`from` [Point](../../Murder/Core/Geometry/Point.html) \
`to` [Point](../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../Murder/Core/Geometry/Point.html) \

#### Resize(IntRectangle)

```csharp
public void Resize(IntRectangle rectangle)
```

This supports resize the grid up to:
**\_** **\_\_**
| | -&gt; | |
|**\_**x | |
|**\_\_**x
or
**\_** **\_**
| x | -&gt; | x |
|**\_**| |**\_**|

            Where x is the bullet point.

**Parameters** \
`rectangle` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### Resize(int, int, Point)

```csharp
public void Resize(int width, int height, Point origin)
```

Resizes the grid to `width`x`height` and moves its origin to `origin`, copying over every cell value that still falls within the new bounds (cells outside the overlap are dropped; newly-exposed cells start at `0`). No-op if the new size matches the current size. Invalidates the auto-tile cache and raises the internal `OnModified` event. Prefer `Resize(IntRectangle)` when you already have the target bounds as a rectangle.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`origin` [Point](../../Murder/Core/Geometry/Point.html) \

#### Set(Point, int, bool)

```csharp
public void Set(Point p, int value, bool overridePreviousValues = false)
```

Sets bits on the cell at local grid position `p`. See `Set(int, int, int, bool)`.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`overridePreviousValues` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Set(int, int, int, bool)

```csharp
public void Set(int x, int y, int value, bool overridePreviousValues = false)
```

Sets bits on the cell at local grid coordinates `x`, `y`, either OR-ing `value` into the existing bitmask (the default) or replacing it outright. Invalidates the auto-tile cache and raises the internal `OnModified` event so dependent rendering/pathfinding data gets rebuilt.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`overridePreviousValues` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetGridPosition(IntRectangle, int)

```csharp
public void SetGridPosition(IntRectangle rect, int value)
```

Sets bits across every cell inside `rect` (in world-space grid coordinates, converted to local coordinates via `Origin`), clamped to the grid's bounds. Used by the editor's rectangle/brush tools to paint a block of tiles in one call.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetGridPosition(Point, int, bool)

```csharp
public void SetGridPosition(Point p, int value, bool overridePreviousValues = false)
```

Sets bits on the cell at world-space grid position `p` (converted to local coordinates via `Origin`).

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`overridePreviousValues` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Unset(Point, int)

```csharp
public void Unset(Point p, int value)
```

Clears bits on the cell at local grid position `p`. See `Unset(int, int, int)`.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Unset(int, int, int)

```csharp
public void Unset(int x, int y, int value)
```

Clears the bits of `value` from the cell at local grid coordinates `x`, `y`. Invalidates the auto-tile cache and raises the internal `OnModified` event so dependent rendering/pathfinding data gets rebuilt.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### UnsetAll(int)

```csharp
public void UnsetAll(int value)
```

Unset all the tiles according to the bitness of `value`.

**Parameters** \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### UnsetGridPosition(IntRectangle, int)

```csharp
public void UnsetGridPosition(IntRectangle rect, int value)
```

Clears bits across every cell inside `rect` (in world-space grid coordinates, converted to local coordinates via `Origin`), clamped to the grid's bounds. Used by the editor's rectangle/brush tools to erase a block of tiles in one call.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### UnsetGridPosition(Point, int)

```csharp
public void UnsetGridPosition(Point p, int value)
```

Clears bits on the cell at world-space grid position `p` (converted to local coordinates via `Origin`).

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### UpdateCache(ImmutableArray\<Entity\>)

```csharp
public void UpdateCache(ImmutableArray<Entity> tileEntities)
```

Forces the auto-tile cache to be rebuilt immediately for all currently-cached tilemap layers, using the current state of `tileEntities`. Call this after tile entities are added/removed/reordered so `GetTile` reflects the new neighbor configuration right away, rather than waiting for a layer-count mismatch to trigger a lazy rebuild.

**Parameters** \
`tileEntities` [ImmutableArray\<Entity\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

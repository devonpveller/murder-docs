# TileGridComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TileGridComponent : IModifiableComponent, IComponent
```

This is a struct that points to a singleton class.
Reactive systems won't be able to subscribe to this component.

**Intent:** Store the tilemap grid data for a room entity — the physical tile layout used by rendering and collision systems.

**Use-case:** Add to a room entity to give it a tile grid; the component declares `[Requires(typeof(RoomComponent))]`, so adding it automatically ensures a [RoomComponent](../../Murder/Components/RoomComponent.html) is present on the same entity as well. Because the underlying `TileGrid` is a mutable class shared by reference, modify tiles through `Grid` directly and subscribe via `Subscribe`/`Unsubscribe` to react to changes, rather than replacing the component wholesale.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public TileGridComponent()
```

Creates an empty 1x1 tile grid at the world origin.

```csharp
public TileGridComponent(Point origin, int width, int height)
```

Creates a new, empty tile grid with the given origin and dimensions.

**Parameters** \
`origin` [Point](../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public TileGridComponent(TileGrid grid)
```

Wraps an existing [TileGrid](../../Murder/Core/TileGrid.html) instance, adopting its origin and dimensions.

**Parameters** \
`grid` [TileGrid](../../Murder/Core/TileGrid.html) \

```csharp
public TileGridComponent(int width, int height)
```

Creates a new, empty tile grid with the given dimensions at the world origin.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Grid

```csharp
public readonly TileGrid Grid;
```

The underlying, mutable tile grid object containing all tile data for this room. This is why `TileGridComponent` implements `IModifiableComponent` instead of being replaced wholesale on every change: systems edit `Grid` in place.

**Returns** \
[TileGrid](../../Murder/Core/TileGrid.html) \

#### Height

```csharp
public readonly int Height;
```

Number of tile rows in `Grid`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Origin

```csharp
public readonly Point Origin;
```

World-space tile coordinate of the grid's top-left corner.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Rectangle

```csharp
public IntRectangle Rectangle { get; }
```

Bounding rectangle of the entire grid in tile coordinates, computed from `Origin`, `Width` and `Height`.

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### Width

```csharp
public readonly int Width;
```

Number of tile columns in `Grid`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### Subscribe(Action)

```csharp
public virtual void Subscribe(Action notification)
```

Registers a callback that fires when tile data in `Grid` is modified.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)

```csharp
public virtual void Unsubscribe(Action notification)
```

Removes a previously registered tile-modification callback.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

⚡

# TileGridComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TileGridComponent : IModifiableComponent, IComponent
```

This is a struct that points to a singleton class.
            Reactive systems won't be able to subscribe to this component.

**Intent:** Store the tilemap grid data for a room entity, providing the physical tile layout used by rendering and collision systems.

**Use-case:** Added automatically to room entities alongside [RoomComponent](../../Murder/Components/RoomComponent.html); modify `Grid` to change tile contents at runtime.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public TileGridComponent()
```

```csharp
public TileGridComponent(Point origin, int width, int height)
```

**Parameters** \
`origin` [Point](../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public TileGridComponent(TileGrid grid)
```

**Parameters** \
`grid` [TileGrid](../../Murder/Core/TileGrid.html) \

```csharp
public TileGridComponent(int width, int height)
```

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Grid
```csharp
public readonly TileGrid Grid;
```

The underlying tile grid object containing all tile data for this room.

**Returns** \
[TileGrid](../../Murder/Core/TileGrid.html) \
#### Height
```csharp
public readonly int Height;
```

Number of tile rows in the grid.

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

Bounding rectangle of the entire grid in tile coordinates.

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
#### Width
```csharp
public readonly int Width;
```

Number of tile columns in the grid.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### Subscribe(Action)
```csharp
public virtual void Subscribe(Action notification)
```

Registers a callback that fires when tile data in the grid is modified.

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
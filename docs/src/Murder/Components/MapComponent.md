# MapComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct MapComponent : IModifiableComponent, IComponent
```

This is a struct that points to a singleton class.
Reactive systems won't be able to subscribe to this component.

**Intent:** Hold the singleton tilemap data for the world, providing all tile, collision, and pathfinding grid information for the current level.

**Use-case:** Added once to the world entity; systems query `Map` to read or modify tile state, and use `Width`/`Height` to determine grid dimensions.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public MapComponent(Point origin, int width, int height)
```

Creates the map with an explicit grid origin, in addition to its size in tiles.

**Parameters** \
`origin` [Point](../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public MapComponent(int width, int height)
```

Creates the map at the default origin (`Point.Zero`) with the given size in tiles.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Height

```csharp
public int Height { get; }
```

Height of the tilemap in grid tiles, delegated directly to `Map.Height`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Map

```csharp
public readonly Map Map;
```

The underlying, mutable tilemap data structure containing all tile, collision, and pathfinding information for the level. Because `Map` is a reference type, systems typically read and mutate the grid directly through it rather than replacing this component wholesale.

**Returns** \
[Map](../../Murder/Core/Map.html) \

#### Width

```csharp
public int Width { get; }
```

Width of the tilemap in grid tiles, delegated directly to `Map.Width`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### Subscribe(Action)

```csharp
public void Subscribe(Action notification)
```

Required by [IModifiableComponent](../../Bang/Components/IModifiableComponent.html), but intentionally a no-op here: `Map` is a mutable reference type that is edited in place, so entity-level component-replacement notifications are never needed to observe changes to it.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)

```csharp
public void Unsubscribe(Action notification)
```

Required by [IModifiableComponent](../../Bang/Components/IModifiableComponent.html), but intentionally a no-op here; see `Subscribe(Action)`.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

⚡

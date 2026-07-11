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
public MapComponent(int width, int height)
```

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Height
```csharp
public int Height { get; }
```

Height of the tilemap in grid tiles.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Map
```csharp
public readonly Map Map;
```

The underlying tilemap data structure containing all tile, collision, and pathfinding information for the level.

**Returns** \
[Map](../../Murder/Core/Map.html) \
#### Width
```csharp
public int Width { get; }
```

Width of the tilemap in grid tiles.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### Subscribe(Action)
```csharp
public virtual void Subscribe(Action notification)
```

Registers a callback invoked when the map data is modified.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)
```csharp
public virtual void Unsubscribe(Action notification)
```

Unregisters a previously subscribed callback from map modification notifications.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡
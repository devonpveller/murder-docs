# HAAStarPathfindComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct HAAStarPathfindComponent : IModifiableComponent, IComponent
```

Holds the world's shared Hierarchical Adaptive A* (`HAAStar`) pathfinding grid, used by `CalculatePathfindSystem` and `PathfindServices` to compute agent paths without rebuilding the hierarchy on every query. It is `[Unique]` (a single instance lives on the world, created once via `PathfindServices` when the map is initialized) and `[RuntimeOnly]`/`[DoNotPersistEntityOnSave]` since it is rebuilt from the current map rather than saved. This is a struct that wraps a reference to a singleton class (`Data`), so mutations to the underlying `HAAStar` instance are visible everywhere the component is fetched; as an `IModifiableComponent` it opts out of Bang's reactive change notifications, since its data mutates in place instead of through component replacement.

**Intent:** Give every pathfinding system and service a single, shared, precomputed pathfinding hierarchy for the current map, instead of each caller building or storing its own copy.

**Use-case:** Added once to the world entity when the map is initialized (see `PathfindServices`); pathfinding systems (like `CalculatePathfindSystem`) fetch it and call `Data.Refresh(map)` after the map changes, then query `Data` for hierarchical A\* paths without rebuilding the hierarchy each frame.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public HAAStarPathfindComponent(int width, int height)
```

Creates the pathfinding component with a new `HAAStar` hierarchy sized for a map of `width` by `height` tiles.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Data

```csharp
public readonly HAAStar Data;
```

The shared Hierarchical A\* data structure used by pathfinding systems and services to compute and cache paths across the map.

**Returns** \
[HAAStar](../../Murder/Core/Ai/HAAStar.html) \

### ⭐ Methods

#### Subscribe(Action)

```csharp
public virtual void Subscribe(Action _)
```

No-op: required by `IModifiableComponent`, but reactive subscriptions are not supported since `Data` mutates in place rather than notifying through component replacement.

**Parameters** \
`_` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)

```csharp
public virtual void Unsubscribe(Action _)
```

No-op: required by `IModifiableComponent`; see `Subscribe`.

**Parameters** \
`_` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

⚡

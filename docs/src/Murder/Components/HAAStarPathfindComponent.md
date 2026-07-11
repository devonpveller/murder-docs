# HAAStarPathfindComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct HAAStarPathfindComponent : IModifiableComponent, IComponent
```

This is a struct that points to a singleton class.
            Reactive systems won't be able to subscribe to this component.

**Intent:** Hold the shared Hierarchical A* pathfinding data structure for the world, allowing agents to query pre-computed path hierarchies.

**Use-case:** Added once to the world entity (it is `[Unique]`); pathfinding systems read `Data` to perform HA* queries without rebuilding the hierarchy each frame.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public HAAStarPathfindComponent(int width, int height)
```

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Data
```csharp
public readonly HAAStar Data;
```

The shared Hierarchical A* data structure used by pathfinding systems to compute optimal paths.

**Returns** \
[HAAStar](../../Murder/Core/Ai/HAAStar.html) \
### ⭐ Methods
#### Subscribe(Action)
```csharp
public virtual void Subscribe(Action _)
```

No-op implementation; reactive subscriptions are not supported for this component.

**Parameters** \
`_` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)
```csharp
public virtual void Unsubscribe(Action _)
```

No-op implementation; reactive subscriptions are not supported for this component.

**Parameters** \
`_` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡
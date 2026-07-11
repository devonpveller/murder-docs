# StateMachineSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class StateMachineSystem : IUpdateSystem, ISystem, IReactiveSystem, IExitSystem
```

Starts, ticks, and cleans up `IStateMachineComponent` state machines on entities, advancing them by scaled or unscaled delta time each update frame.

**Intent:** The main driver for entity state machines — it initializes them on startup, steps them forward each frame, and disposes them when entities are removed.

**Use-case:** Required in any world that uses `IStateMachineComponent`; include once and it manages all state machine entities automatically.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [IExitSystem](../../Bang/Systems/IExitSystem.html)_

### ⭐ Constructors
```csharp
public StateMachineSystem()
```

### ⭐ Methods
#### Exit(Context)
```csharp
public virtual void Exit(Context context)
```
Disposals all active state machine instances when the world exits.
**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

No-op reactive stub; state machine startup is handled by `Start`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

No-op reactive stub required by `IReactiveSystem`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Disposes state machine instances on removed entities.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Update(Context)
```csharp
public virtual void Update(Context context)
```

Ticks every active state machine by the appropriate delta time (scaled or unscaled), or by a large value when the game is skipping delta time in a cutscene.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡
# StateMachineOnPauseSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class StateMachineOnPauseSystem : IUpdateSystem, ISystem, IReactiveSystem, IExitSystem
```

Updates state machines on entities that also have `DoNotPauseComponent`, advancing them with unscaled delta time even when the world is paused.

**Intent:** Keeps designated state machines ticking during world pause so critical logic (e.g., menu flows, cutscene state) is unaffected by the pause state.

**Use-case:** Mark an entity with `DoNotPauseComponent` alongside its state machine component to ensure the machine continues advancing during gameplay pauses.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [IExitSystem](../../Bang/Systems/IExitSystem.html)_

### ⭐ Constructors
```csharp
public StateMachineOnPauseSystem()
```

### ⭐ Methods
#### Exit(Context)
```csharp
public virtual void Exit(Context context)
```
Disposals all state machine instances when the world exits, ensuring any unmanaged resources are released.
**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

No-op reactive stub required by the `IReactiveSystem` interface.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

No-op reactive stub required by the `IReactiveSystem` interface.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

No-op reactive stub required by the `IReactiveSystem` interface.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Update(Context)
```csharp
public virtual void Update(Context context)
```

Ticks each active state machine by unscaled delta time so it continues advancing during gameplay pause.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡
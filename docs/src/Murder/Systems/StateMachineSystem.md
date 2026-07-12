# StateMachineSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class StateMachineSystem : IStartupSystem, IUpdateSystem, IReactiveSystem, IExitSystem, ISystem
```

Filtered and watched on `IStateMachineComponent`. Starts, ticks, and cleans up state machines on entities, advancing them each update by scaled or unscaled delta time depending on whether the entity carries `UnscaledDeltaTimeComponent`.

**Intent:** The main driver for entity state machines (`Bang.StateMachines.IStateMachineComponent`, typically created via `StateMachine<T>`) — it calls `Start()` on each routine once, ticks them forward every frame while the world is running, resets them when their owning entity deactivates, and disposes them when the entity (or the world) is destroyed. Designed to be subclassed: `ShouldUpdate` and the protected `Update(Entity)` overload let a derived system gate or customize per-entity ticking (`StateMachineOnPauseSystem` implements the equivalent pause-time behavior as a separate sibling class rather than a subclass, but a game-specific system could subclass `StateMachineSystem` directly to add, e.g., a "only tick while visible on screen" condition).

**Use-case:** Required in any world that uses `IStateMachineComponent`; include once and it manages all state machine entities automatically. Pair with `StateMachineOnPauseSystem` (marked `[OnPause]`) if some state machines, tagged with `DoNotPauseComponent`, need to keep ticking while the world is paused.

**Implements:** _[IStartupSystem](../../Bang/Systems/IStartupSystem.html), [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [IExitSystem](../../Bang/Systems/IExitSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public StateMachineSystem()
```

### ⭐ Methods

#### Exit(Context)

```csharp
public virtual void Exit(Context context)
```

Disposes every state machine instance (that implements `IDisposable`) still matching the filter when the world exits, ensuring any unmanaged resources held by the routine are released.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Currently a no-op (the cleanup hook it calls is intentionally empty); state machine startup is instead handled by `Start`, which runs once when the system is added to the world.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnDeactivated(World, ImmutableArray<T>)

```csharp
public virtual void OnDeactivated(World world, ImmutableArray<T> entities)
```

Calls `Reset()` on each deactivated entity's state machine, so its internal state does not linger stale while the entity is inactive and cause unexpected behavior if the entity is later reactivated.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Currently a no-op (the cleanup hook it calls is intentionally empty).

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Currently a no-op (the cleanup hook it calls is intentionally empty); routine disposal on removal is instead handled by the entity destruction path and `Exit`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### ShouldUpdate(Entity)

```csharp
protected virtual bool ShouldUpdate(Entity e)
```

Hook that gates whether `Update(Entity)` should tick a given entity's state machine this frame; always returns `true` in the base implementation. Override in a subclass to add custom conditions (e.g. skip entities outside the camera, or entities flagged as frozen) without having to reimplement delta-time selection.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Start(Context)

```csharp
public virtual void Start(Context context)
```

Calls `Start()` on every matching entity's state machine routine once, when the system is first added to the world (e.g. on scene load), giving each routine a chance to run its initial logic before the first `Update`.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### Update(Context)

```csharp
public virtual void Update(Context context)
```

Calls `Update(Entity)` for every matching entity.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### Update(Entity)

```csharp
protected void Update(Entity e)
```

Ticks a single entity's state machine, provided `ShouldUpdate(e)` returns `true`. Uses `Game.UnscaledDeltaTime` if the entity has an `UnscaledDeltaTimeComponent`, otherwise `Game.DeltaTime`; if the game is currently skipping delta time on update (e.g. fast-forwarding through a cutscene), a fixed large delta time (`100`) is used instead so the routine resolves immediately. Exposed as `protected` so a subclass's overridden `Update(Context)` can still drive individual entities through the same logic.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

⚡

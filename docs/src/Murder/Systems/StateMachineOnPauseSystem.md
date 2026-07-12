# StateMachineOnPauseSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class StateMachineOnPauseSystem : IUpdateSystem, IExitSystem, ISystem
```

Marked with `[OnPause]`, meaning this system is only active while the world is paused. Filtered to entities that have both an `IStateMachineComponent` and a `DoNotPauseComponent`, it advances those state machines with unscaled delta time so they keep running even though gameplay is frozen.

**Intent:** Keeps designated state machines ticking while the world is paused, so pause-exempt logic (e.g., a pause menu's own state machine, an animated cutscene overlay, background ambient behavior) is unaffected by the pause state. This is the pause-time counterpart to `StateMachineSystem`, which only runs while the world is unpaused.

**Use-case:** Mark an entity with `DoNotPauseComponent` alongside its `IStateMachineComponent` to ensure the machine continues advancing during gameplay pauses; this system (registered by the pause feature via `[OnPause]`) then picks it up automatically instead of `StateMachineSystem`.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [IExitSystem](../../Bang/Systems/IExitSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public StateMachineOnPauseSystem()
```

### ⭐ Methods

#### Exit(Context)

```csharp
public virtual void Exit(Context context)
```

Disposes every state machine instance (that implements `IDisposable`) still matching the filter when the world exits, ensuring any unmanaged resources held by the routine are released.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### Update(Context)

```csharp
public virtual void Update(Context context)
```

Ticks each matching entity's state machine using `Game.UnscaledDeltaTime`, so it continues advancing normally regardless of the world's pause/time-scale state.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡

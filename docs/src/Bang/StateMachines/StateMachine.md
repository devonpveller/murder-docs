# StateMachine

**Namespace:** Bang.StateMachines \
**Assembly:** Bang.dll

```csharp
public abstract class StateMachine
```

Base class for a scripted, coroutine-style behavior driven off an entity — the tool of choice for dialogue, cutscenes, timed sequences and simple AI, anywhere "do this, then wait, then do that" reads more naturally as imperative code than as a handful of ECS systems.
            It is sort-of anti-pattern of ECS at this point. This is a trade-off
            between adding content and using ECS at the core of the game.

A subclass models each of its states as a method with the signature `IEnumerator<Wait> MyState()`, written as a C# iterator: `yield return` a [Wait](../../Bang/StateMachines/Wait.html) value (e.g. `Wait.ForSeconds(float)`, `Wait.ForMessage<T>()`, `Wait.NextFrame`) to suspend the routine until that condition is satisfied, then resume execution right after that line on the next eligible tick — exactly like a coroutine. The constructor picks the initial state by calling [State(Func\<TResult\>)](../../Bang/StateMachines/StateMachine.html#statefunctresult) with the method group (e.g. `State(Talk)`), and later transitions are made with [GoTo](../../Bang/StateMachines/StateMachine.html#gotofunctresult)/[Transition](../../Bang/StateMachines/StateMachine.html#transitionfunctresult). The engine drives all of this by wrapping the subclass in a [StateMachineComponent\<T\>](../../Bang/StateMachines/StateMachineComponent-1.html) and attaching it to an entity (see `Entity.SetStateMachine`).

A minimal, real example is `Murder.StateMachines.CoroutineStateMachine` (`src\Murder\StateMachines\CoroutineStateMachine.cs`), whose only state simply forwards to a caller-supplied routine:

```csharp
public class CoroutineStateMachine : StateMachine
{
    private readonly IEnumerator<Wait> _routine;

    public CoroutineStateMachine(IEnumerator<Wait> routine)
    {
        _routine = routine;
        State(Run);
    }

    private IEnumerator<Wait> Run()
    {
        yield return Wait.ForRoutine(_routine);
    }
}
```

A more involved example is `Murder.StateMachines.Dialogs.DialogStateMachine` (`src\Murder\StateMachines\Dialogs\DialogStateMachine.cs`), which drives a dialogue/cutscene loop with a single `Talk()` state that repeatedly fetches the next line, publishes it as a component on the entity, and then `yield return`s a message wait (e.g. `Wait.ForMessage<NextDialogMessage>()`) until the player/UI signals it is time to advance — throwing an [InvalidStateMachineException](../../Bang/StateMachines/InvalidStateMachineException.html) from `OnStart` if the entity is missing the situation it needs to begin.

A developer or autonomous agent authoring new scripted behavior should: subclass `StateMachine`, write one method per state returning `IEnumerator<Wait>`, call `State(InitialState)` from the constructor, and drive pacing entirely with `yield return Wait.…` rather than manual timers or flags — the base class takes care of resuming the routine at the right time, listening for messages, and cleaning everything up when the routine finishes.

### ⭐ Constructors
```csharp
protected StateMachine()
```

Implicit parameterless constructor. Subclasses should call [State(Func\<TResult\>)](../../Bang/StateMachines/StateMachine.html#statefunctresult) from their own constructor to pick the routine that represents their initial state; until that happens the state machine has no active routine and cannot be ticked.

### ⭐ Properties
#### Entity
```csharp
protected Entity Entity;
```

Entity of the state machine.
            Initialized in [StateMachine.Initialize(Bang.World,Bang.Entities.Entity)](../../Bang/StateMachines/StateMachine.html). Every state method can read this to inspect or mutate the components of the entity the state machine is attached to.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
#### LastMessage
```csharp
protected IMessage LastMessage { get; }
```

The message instance that satisfied the most recent `Wait.ForMessage<T>()`/`Wait.ForMessage<T>(Entity)` wait. Read this from the state right after resuming from a message wait (or from [OnMessage(IMessage)](../../Bang/StateMachines/StateMachine.html#onmessageimessage)) to inspect the payload of the message that woke it up.

**Returns** \
[IMessage](../../Bang/Components/IMessage.html) \
#### Name
```csharp
public string Name { get; private set; }
```

Name of the active state. Used for debug.
            This is the method name passed to [State(Func\<TResult\>)](../../Bang/StateMachines/StateMachine.html#statefunctresult), and — when [PersistStateOnSave](../../Bang/StateMachines/StateMachine.html#persiststateonsave) is `true` — the value that gets serialized so the same state can be resumed after loading a save.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### PersistStateOnSave
```csharp
protected virtual bool PersistStateOnSave { get; }
```

Whether the state machine active state should be persisted on serialization. Defaults to `true`; override and return `false` for state machines whose state should always restart from scratch instead of resuming mid-way after a save/load (for example one whose states are not safe/meaningful to resume without the transient context that led to them).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### World
```csharp
protected World World;
```

World of the state machine.
            Initialized in [StateMachine.Initialize(Bang.World,Bang.Entities.Entity)](../../Bang/StateMachines/StateMachine.html). Gives state routines access to the rest of the ECS (querying other entities, adding new ones, etc.) while they run.

**Returns** \
[World](../../Bang/World.html) \
### ⭐ Methods
#### GoTo(Func<TResult>)
```csharp
protected virtual Wait GoTo(Func<TResult> routine)
```

Redirects the state machine to a new [routine](../../Bang/StateMachines/StateMachine.html).
            Switches state immediately and ticks the new routine right away, returning the [Wait](../../Bang/StateMachines/Wait.html) it yields. This is meant to be called (and its result `yield return`'d) from within a state's own routine — e.g. `yield return GoTo(NextState);` — to hand off control to another state without waiting for the next engine tick. For transitions triggered from outside the routine (e.g. from [OnMessage(IMessage)](../../Bang/StateMachines/StateMachine.html#onmessageimessage)), use [Transition](../../Bang/StateMachines/StateMachine.html#transitionfunctresult) or [TransitionAndTick](../../Bang/StateMachines/StateMachine.html#transitionandtickfunctresult) instead.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) — target routine (new state). \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) — the `Wait` yielded by the first tick of `routine`. \

#### OnDestroyed()
```csharp
public virtual void OnDestroyed()
```

Clean up right before the state machine gets cleaned up.
            Callers must call the base implementation. The base implementation unsubscribes from entity messages and disposes the current routine (and any nested routines it was waiting on via `Wait.ForRoutine`). Override to release any additional resources a subclass holds, always calling `base.OnDestroyed()`.

#### OnMessage(IMessage)
```csharp
protected virtual void OnMessage(IMessage message)
```

Implemented by state machine implementations that want to listen to message
            notifications from outer systems. Called for every message sent to the owner entity while the state machine is subscribed (see [Subscribe()](../../Bang/StateMachines/StateMachine.html#subscribe)), regardless of whether a routine is actively `yield return`ing a matching `Wait.ForMessage<T>()` — override this to react to messages that should affect the state machine without necessarily being the thing a routine is currently waiting on.

**Parameters** \
`message` [IMessage](../../Bang/Components/IMessage.html) \

#### OnStart()
```csharp
protected virtual void OnStart()
```

Initialize the state machine. Called before the first [StateMachine.Tick(System.Single)](../../Bang/StateMachines/StateMachine.html) call.
            This is the right place to validate that the entity has whatever components the state machine depends on, throwing an [InvalidStateMachineException](../../Bang/StateMachines/InvalidStateMachineException.html) if a required precondition is missing — see `Murder.StateMachines.Dialogs.DialogStateMachine.OnStart`, which throws when the entity has no situation to talk from.

#### ResetCurrentState()
```csharp
public void ResetCurrentState()
```

This resets the current state of the state machine back to the beginning of that same state. Re-invokes the routine method for the current (or last persisted) state from scratch, discarding any progress within it — as if [GoTo](../../Bang/StateMachines/StateMachine.html#gotofunctresult) had been called again with the same state. This is what backs `IStateMachineComponent.Reset`, which the engine may call when a state machine component is reused, e.g. after being restored from a save that only persisted the state's name (see [PersistStateOnSave](../../Bang/StateMachines/StateMachine.html#persiststateonsave)).

#### State(Func<TResult>)
```csharp
protected void State(Func<TResult> routine)
```

Set the current state of the state machine with [routine](../../Bang/StateMachines/StateMachine.html).
            This is the primitive every other transition helper ([GoTo](../../Bang/StateMachines/StateMachine.html#gotofunctresult), [Transition](../../Bang/StateMachines/StateMachine.html#transitionfunctresult), [TransitionAndTick](../../Bang/StateMachines/StateMachine.html#transitionandtickfunctresult)) ultimately calls. Subclasses typically call it once, directly, from their constructor to pick the initial state (for example `State(Talk)`), passing the method group of an `IEnumerator<Wait>`-returning iterator method that implements that state. Disposes the previous routine (and any nested routines it was waiting on) before invoking the new one, and records `routine`'s method name as [Name](../../Bang/StateMachines/StateMachine.html#name) for debugging/persistence purposes.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### Subscribe()
```csharp
public void Subscribe()
```

Starts listening to messages sent to the owner [Entity](../../Bang/Entities/Entity.html) so that [OnMessage(IMessage)](../../Bang/StateMachines/StateMachine.html#onmessageimessage) and any pending `Wait.ForMessage<T>()` can react to them. This is wired up automatically by [StateMachineComponent\<T\>](../../Bang/StateMachines/StateMachineComponent-1.html) when the component is attached; callers generally do not need to invoke this directly.

#### Transition(Func<TResult>)
```csharp
protected virtual void Transition(Func<TResult> routine)
```

Redirects the state machine to a new [routine](../../Bang/StateMachines/StateMachine.html) without doing
            a tick. If called while the state machine is in the middle of ticking, the transition is queued and only applied once that tick finishes (so a routine can never be swapped out from under itself mid-tick); otherwise it takes effect immediately, but the new routine's first `yield return` will only run on the next call to `Tick`.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) — target routine (new state). \

#### TransitionAndTick(Func<TResult>)
```csharp
protected virtual void TransitionAndTick(Func<TResult> routine)
```

Redirects the state machine to a new [routine](../../Bang/StateMachines/StateMachine.html) and, unlike [Transition](../../Bang/StateMachines/StateMachine.html#transitionfunctresult), immediately ticks it afterwards (unless a tick is already in progress, in which case the transition is simply queued like a normal `Transition` and picked up once the current tick finishes). Use this when a state change should take effect within the same frame it was requested, instead of waiting for the next engine tick.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) — target routine (new state). \

#### Unsubscribe()
```csharp
public void Unsubscribe()
```

Stops listening to messages sent to the owner [Entity](../../Bang/Entities/Entity.html), undoing [Subscribe()](../../Bang/StateMachines/StateMachine.html#subscribe). This is wired up automatically by [StateMachineComponent\<T\>](../../Bang/StateMachines/StateMachineComponent-1.html) when the component is removed/replaced; callers generally do not need to invoke this directly.



⚡

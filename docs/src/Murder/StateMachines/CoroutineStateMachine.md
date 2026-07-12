# CoroutineStateMachine

**Namespace:** Murder.StateMachines \
**Assembly:** Murder.dll

```csharp
public class CoroutineStateMachine : StateMachine
```

This CANNOT and WONT be serialized it is just a bad idea. Remember, we can't (or don't want to) serialize lambdas.

**Intent:** Wraps a caller-supplied `IEnumerator<Wait>` routine inside a `StateMachine` so any one-off, iterator-based coroutine can be driven by the Bang ECS scheduler without needing a dedicated `StateMachine` subclass. Its only state (`Run`) does nothing but `yield return Wait.ForRoutine(_routine)`, forwarding every tick straight through to the supplied routine.

**Use-case:** You rarely construct this directly — call `world.RunCoroutine(routine)`/`entity.RunCoroutine(routine)` from `CoroutineServices` instead, which wraps the routine in a `CoroutineStateMachine` and attaches it via `Entity.SetStateMachine` for you. Use this when a short one-off sequence of `yield return Wait...` steps is needed and writing a full `StateMachine` subclass would be overkill. Marked `[RuntimeOnly]` since a lambda-backed routine cannot be meaningfully serialized into a save.

**Implements:** _[StateMachine](../../Bang/StateMachines/StateMachine.html)_

### ⭐ Constructors

```csharp
public CoroutineStateMachine()
```

Parameterless constructor used only as a safety net (e.g. by generic/reflection-based instantiation); it runs a routine that immediately yields `Wait.Stop`, so a `CoroutineStateMachine` created this way finishes without doing anything. Prefer the `IEnumerator<Wait>` overload.

```csharp
public CoroutineStateMachine(IEnumerator<Wait> routine)
```

Creates a coroutine state machine that runs `routine` to completion, one `Wait` at a time, exactly as if it had been written as a state method on a `StateMachine` subclass.

**Parameters** \
`routine` [IEnumerator\<Wait\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \

### ⭐ Properties

#### Entity

```csharp
protected Entity Entity;
```

Inherited from `StateMachine`. Entity of the state machine, initialized when the state machine starts; available for the wrapped routine to inspect or mutate via closures.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### LastMessage

```csharp
protected IMessage LastMessage { get; }
```

Inherited from `StateMachine`. The message instance that satisfied the most recent `Wait.ForMessage<T>()` wait; read this right after resuming from a message wait to inspect the payload.

**Returns** \
[IMessage](../../Bang/Components/IMessage.html) \

#### Name

```csharp
public string Name { get; }
```

Inherited from `StateMachine`. Name of the active state, used for debugging — for `CoroutineStateMachine` this is always `"Run"`, since it has no other states.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PersistStateOnSave

```csharp
protected virtual bool PersistStateOnSave { get; }
```

Inherited from `StateMachine`, not overridden by `CoroutineStateMachine`. Whether the active state should be persisted on serialization; irrelevant in practice since the whole class is `[RuntimeOnly]` and never serialized.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### World

```csharp
protected World World;
```

Inherited from `StateMachine`. World of the state machine, initialized when the state machine starts; available for the wrapped routine to inspect via closures.

**Returns** \
[World](../../Bang/World.html) \

### ⭐ Methods

#### GoTo(Func<TResult>)

```csharp
protected virtual Wait GoTo(Func<TResult> routine)
```

Inherited from `StateMachine`, not used by `CoroutineStateMachine` (which has only one state). Redirects the state machine to a new routine immediately, ticking it right away.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### OnDestroyed()

```csharp
public virtual void OnDestroyed()
```

Inherited from `StateMachine`, not overridden. Unsubscribes from entity messages and disposes the wrapped routine (and any nested routines it was waiting on) when the state machine finishes or the entity is destroyed.

#### OnMessage(IMessage)

```csharp
protected virtual void OnMessage(IMessage message)
```

Inherited from `StateMachine`, not overridden by `CoroutineStateMachine` — the base no-op implementation is used, since the wrapped routine has no way to receive an override for it. If the routine needs to react to messages, it must do so itself via `Wait.ForMessage<T>()`.

**Parameters** \
`message` [IMessage](../../Bang/Components/IMessage.html) \

#### OnStart()

```csharp
protected virtual void OnStart()
```

Inherited from `StateMachine`, not overridden by `CoroutineStateMachine`. Called once before the first tick; the base no-op implementation is used.

#### ResetCurrentState()

```csharp
public void ResetCurrentState()
```

Inherited from `StateMachine`. Restarts the current state (`Run`) from the beginning, discarding any progress the wrapped routine had made.

#### State(Func<TResult>)

```csharp
protected void State(Func<TResult> routine)
```

Inherited from `StateMachine`. The primitive `CoroutineStateMachine`'s constructor calls once, with `Run`, to install the routine-forwarding state.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### Subscribe()

```csharp
public void Subscribe()
```

Inherited from `StateMachine`. Starts listening to messages sent to the owning entity; wired up automatically by `StateMachineComponent<T>` when attached.

#### Transition(Func<TResult>)

```csharp
protected virtual void Transition(Func<TResult> routine)
```

Inherited from `StateMachine`, not used by `CoroutineStateMachine`. Redirects to a new routine without ticking it immediately.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### TransitionAndTick(Func<TResult>)

```csharp
protected virtual void TransitionAndTick(Func<TResult> routine)
```

Inherited from `StateMachine`, not used by `CoroutineStateMachine`. Redirects to a new routine and ticks it immediately (unless already ticking).

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### Unsubscribe()

```csharp
public void Unsubscribe()
```

Inherited from `StateMachine`. Stops listening to messages sent to the owning entity, undoing `Subscribe`.

⚡

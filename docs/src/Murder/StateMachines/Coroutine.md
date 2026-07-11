# Coroutine

**Namespace:** Murder.StateMachines \
**Assembly:** Murder.dll

```csharp
public class Coroutine : StateMachine
```

This CANNOT and WONT be serialized it is just a bad idea. Remember, we can't (or don't want to) serialize lambdas.

**Intent:** Wraps a caller-supplied `IEnumerator<Wait>` routine inside a `StateMachine` so any iterator-based coroutine can be driven by the Bang ECS scheduler without needing a dedicated class.

**Use-case:** Create a one-off coroutine in-place via `new Coroutine(MyMethod())` and attach it as a state-machine component to a temporary entity rather than writing a full `StateMachine` subclass.

**Implements:** _[StateMachine](../../Bang/StateMachines/StateMachine.html)_

### ⭐ Constructors
```csharp
public Coroutine()
```

```csharp
public Coroutine(IEnumerator<T> routine)
```
Creates a coroutine state machine that will run `routine` until it completes.

**Parameters** \
`routine` [IEnumerator\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \

### ⭐ Properties
#### Entity
```csharp
protected Entity Entity;
```
The ECS entity that owns this state machine, set by the Bang framework on start.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
#### Name
```csharp
public string Name { get; }
```
Debug name of this state machine (typically the class name).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### PersistStateOnSave
```csharp
protected virtual bool PersistStateOnSave { get; }
```
When `false` (the default for `Coroutine`), the state machine state is not persisted across save/load.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### World
```csharp
protected World World;
```
The ECS world in which this state machine is running.

**Returns** \
[World](../../Bang/World.html) \
### ⭐ Methods
#### OnMessage(IMessage)
```csharp
protected virtual void OnMessage(IMessage message)
```
Called when a message is dispatched to the owning entity; override to handle specific messages.

**Parameters** \
`message` [IMessage](../../Bang/Components/IMessage.html) \

#### OnStart()
```csharp
protected virtual void OnStart()
```
Called once when the state machine is first activated; override to perform initialization.

#### Transition(Func<TResult>)
```csharp
protected virtual void Transition(Func<TResult> routine)
```
Transitions the state machine to the given routine immediately, without waiting for the current tick to finish.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### GoTo(Func<TResult>)
```csharp
protected virtual Wait GoTo(Func<TResult> routine)
```
Yields a `Wait` that transitions to `routine` on the next tick.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### Reset()
```csharp
protected void Reset()
```
Resets the state machine back to its initial state.

#### State(Func<TResult>)
```csharp
protected void State(Func<TResult> routine)
```
Registers `routine` as the current entry-point state; called in the constructor to set the initial routine.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### SwitchState(Func<TResult>)
```csharp
protected void SwitchState(Func<TResult> routine)
```

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### OnDestroyed()
```csharp
public virtual void OnDestroyed()
```

#### Subscribe(Action)
```csharp
public void Subscribe(Action notification)
```

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)
```csharp
public void Unsubscribe(Action notification)
```

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡
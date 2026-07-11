# DialogStateMachine

**Namespace:** Murder.StateMachines \
**Assembly:** Murder.dll

```csharp
public class DialogStateMachine : StateMachine
```

State machine that drives dialogue playback for a character entity, feeding `DialogLine` components to the entity each tick and awaiting player choices.

**Intent:** Manages the full lifecycle of an in-game dialogue exchange, from fetching the next line to waiting for player input and cleaning up after the conversation ends.

**Use-case:** Added automatically to entities that have a `SituationComponent`; it will run through the character's dialogue tree and destroy itself (or remove the state-machine component) when the dialogue is exhausted.

**Implements:** _[StateMachine](../../Bang/StateMachines/StateMachine.html)_

### ⭐ Constructors
```csharp
public DialogStateMachine()
```

```csharp
public DialogStateMachine(bool destroyAfterDone)
```
Creates a dialog state machine; when `destroyAfterDone` is `false`, the state-machine component is removed instead of destroying the entity.

**Parameters** \
`destroyAfterDone` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### Entity
```csharp
protected Entity Entity;
```
The ECS entity running this dialogue state machine.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
#### Name
```csharp
public string Name { get; }
```
Debug name of this state machine.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### PersistStateOnSave
```csharp
protected virtual bool PersistStateOnSave { get; }
```
When `false`, the dialogue state is not persisted across save/load cycles.

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
Called when a message is dispatched to the owning entity; handles `PickChoiceMessage` to advance choices.

**Parameters** \
`message` [IMessage](../../Bang/Components/IMessage.html) \

#### OnStart()
```csharp
protected virtual void OnStart()
```
Initializes the character runtime from the entity's `SituationComponent`.

#### Transition(Func<TResult>)
```csharp
protected virtual void Transition(Func<TResult> routine)
```
Transitions immediately to a new routine.

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
Resets this state machine back to its initial state.

#### State(Func<TResult>)
```csharp
protected void State(Func<TResult> routine)
```
Registers `routine` as the current entry-point state.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### SwitchState(Func<TResult>)
```csharp
protected void SwitchState(Func<TResult> routine)
```
Switches to the given routine, replacing the current state.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### Talk()
```csharp
public IEnumerator<T> Talk()
```
Main dialogue loop; fetches lines from the character runtime and sets `LineComponent` on the entity, yielding until the player advances.

**Returns** \
[IEnumerator\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \

#### OnDestroyed()
```csharp
public virtual void OnDestroyed()
```
Called when the owning entity is destroyed; unsubscribes all notification listeners.

#### Subscribe(Action)
```csharp
public void Subscribe(Action notification)
```
Registers a callback that will be invoked whenever the dialogue state changes.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)
```csharp
public void Unsubscribe(Action notification)
```
Removes a previously registered change notification callback.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡
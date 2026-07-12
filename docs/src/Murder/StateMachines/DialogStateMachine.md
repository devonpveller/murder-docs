# DialogStateMachine

**Namespace:** Murder.StateMachines \
**Assembly:** Murder.dll

```csharp
public class DialogStateMachine : StateMachine
```

State machine that drives dialogue playback for a character entity, feeding `LineComponent`/`ChoiceComponent` to the entity each tick and awaiting player input to advance.

**Intent:** Owns the full lifecycle of an in-game dialogue exchange: on start, builds a `CharacterRuntime` from the entity's `SituationComponent`; its single `Talk` state then repeatedly asks that runtime for the next line or choice, publishes it as a component on the entity, and `yield return`s a message wait (`NextDialogMessage` for lines, `PickChoiceMessage` for choices) until the player/UI signals it's time to continue — destroying (or removing the state machine from) the entity once the dialogue tree is exhausted.

**Use-case:** Added (typically by dialogue-triggering interactions/services) to entities that have a `SituationComponent` describing which character and situation to talk from; the state machine takes over from there and needs no further driving by game code. Marked `[RuntimeOnly]` because its live `CharacterRuntime` state cannot be meaningfully serialized into a save — a saved game resumes dialogue by re-triggering it, not by restoring this state machine.

**Implements:** _[StateMachine](../../Bang/StateMachines/StateMachine.html)_

### ⭐ Constructors

```csharp
public DialogStateMachine()
```

Creates a dialog state machine that destroys its entity once the dialogue is exhausted (equivalent to `DialogStateMachine(true)`).

```csharp
public DialogStateMachine(bool destroyAfterDone)
```

Creates a dialog state machine; when `destroyAfterDone` is `false`, the entity is kept alive and only the `LineComponent`/state-machine component are removed once the dialogue ends, instead of destroying the whole entity.

**Parameters** \
`destroyAfterDone` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### Entity

```csharp
protected Entity Entity;
```

Inherited from `StateMachine`. The entity running this dialogue state machine; `Talk` reads its `SituationComponent`/writes `LineComponent`/`ChoiceComponent` on it every step.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### LastMessage

```csharp
protected IMessage LastMessage { get; }
```

Inherited from `StateMachine`. The message instance that satisfied the most recent message wait (e.g. the `NextDialogMessage`/`PickChoiceMessage` that let `Talk` continue).

**Returns** \
[IMessage](../../Bang/Components/IMessage.html) \

#### Name

```csharp
public string Name { get; }
```

Inherited from `StateMachine`. Name of the active state, used for debugging — always `"Talk"` for `DialogStateMachine`, since it has only one state.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PersistStateOnSave

```csharp
protected virtual bool PersistStateOnSave { get; }
```

Inherited from `StateMachine`, not overridden by `DialogStateMachine`. In practice irrelevant since the class is `[RuntimeOnly]` and never serialized.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### World

```csharp
protected World World;
```

Inherited from `StateMachine`. The ECS world this dialogue is running in; passed to `CharacterRuntime.NextLine`/`DoChoice` each step.

**Returns** \
[World](../../Bang/World.html) \

### ⭐ Methods

#### GoTo(Func<TResult>)

```csharp
protected virtual Wait GoTo(Func<TResult> routine)
```

Inherited from `StateMachine`, not used by `DialogStateMachine` (which has only one state). Redirects to a new routine, ticking it right away.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### OnDestroyed()

```csharp
public virtual void OnDestroyed()
```

Inherited from `StateMachine`, not overridden. Unsubscribes from entity messages and disposes the `Talk` routine when the state machine finishes or the entity is destroyed.

#### OnMessage(IMessage)

```csharp
protected override void OnMessage(IMessage message)
```

Overridden to capture the player's answer: when `message` is a `PickChoiceMessage`, stores its `Choice` index so that the `Talk` routine (which is separately waiting on that same message via `Wait.ForMessage<PickChoiceMessage>()`) can read it back and call `CharacterRuntime.DoChoice` once it resumes.

**Parameters** \
`message` [IMessage](../../Bang/Components/IMessage.html) \

#### OnStart()

```csharp
protected override void OnStart()
```

Overridden to initialize the dialogue: reads the entity's `SituationComponent` and builds a `CharacterRuntime` from it via `DialogueServices.CreateCharacterFrom`, throwing an `InvalidStateMachineException` if the entity has no `SituationComponent` at all. If the character/situation cannot be resolved, destroys the entity instead of crashing.

#### ResetCurrentState()

```csharp
public void ResetCurrentState()
```

Inherited from `StateMachine`. Restarts the current state (`Talk`) from the beginning, discarding any progress in the current line/choice.

#### State(Func<TResult>)

```csharp
protected void State(Func<TResult> routine)
```

Inherited from `StateMachine`. The primitive `DialogStateMachine`'s constructor calls once, with `Talk`, to install the dialogue loop as the initial (and only) state.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### Subscribe()

```csharp
public void Subscribe()
```

Inherited from `StateMachine`. Starts listening to messages sent to the owning entity; wired up automatically when the state machine is attached, so `OnMessage` receives `PickChoiceMessage`.

#### Talk()

```csharp
public IEnumerator<Wait> Talk()
```

The state machine's single state and main dialogue loop. Repeatedly calls `CharacterRuntime.NextLine`: for a text line, sets `LineComponent` on the entity and waits a frame then for `NextDialogMessage`; for a delayed (non-text) line, waits `Line.Delay` seconds instead; for a choice, sets `ChoiceComponent`, waits a frame then for `PickChoiceMessage`, then applies the chosen option via `CharacterRuntime.DoChoice`. When the character runtime has no more lines, either destroys the entity or removes its `LineComponent`/state machine, depending on the `destroyAfterDone` constructor argument.

**Returns** \
[IEnumerator\<Wait\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \

#### Transition(Func<TResult>)

```csharp
protected virtual void Transition(Func<TResult> routine)
```

Inherited from `StateMachine`, not used by `DialogStateMachine`. Redirects to a new routine without ticking it immediately.

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### TransitionAndTick(Func<TResult>)

```csharp
protected virtual void TransitionAndTick(Func<TResult> routine)
```

Inherited from `StateMachine`, not used by `DialogStateMachine`. Redirects to a new routine and ticks it immediately (unless already ticking).

**Parameters** \
`routine` [Func\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-1?view=net-7.0) \

#### Unsubscribe()

```csharp
public void Unsubscribe()
```

Inherited from `StateMachine`. Stops listening to messages sent to the owning entity, undoing `Subscribe`.

⚡

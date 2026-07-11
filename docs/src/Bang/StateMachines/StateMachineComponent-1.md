# StateMachineComponent\<T\>

**Namespace:** Bang.StateMachines \
**Assembly:** Bang.dll

```csharp
public sealed struct StateMachineComponent<T> : IStateMachineComponent, IComponent, IModifiableComponent
```

The component that actually gets attached to an [Entity](../../Bang/Entities/Entity.html) to give it scripted, coroutine-style behavior. This is a thin adapter: it wraps a concrete [StateMachine](../../Bang/StateMachines/StateMachine.html) subclass `T` and forwards every [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html) call to it, so the actual state/behavior logic can live in plain, testable C# on `T` instead of on the component itself (Bang components are expected to be simple structs).

`T` must be a [StateMachine](../../Bang/StateMachines/StateMachine.html) subclass with a parameterless constructor, so the engine can create a default instance when one isn't supplied explicitly (e.g. during deserialization). Attach one with `entity.SetStateMachine(new StateMachineComponent<MyStateMachine>())`, or, if the routine needs constructor arguments (e.g. a pre-built `IEnumerator<Wait>` for `CoroutineStateMachine`), `new StateMachineComponent<T>(new T(...))` — see `Murder.Services.CoroutineServices.RunCoroutine`, which does exactly that:

```csharp
e.SetStateMachine(new StateMachineComponent<CoroutineStateMachine>(new CoroutineStateMachine(routine)));
```

**Implements:** _[IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html), [IComponent](../../Bang/Components/IComponent.html), [IModifiableComponent](../../Bang/Components/IModifiableComponent.html)_

### ⭐ Constructors
```csharp
public StateMachineComponent<T>()
```

Creates a new [StateMachineComponent\<T\>](../../Bang/StateMachines/StateMachineComponent-1.html) wrapping a brand new `T` instance (via its parameterless constructor). This is the constructor used when the routine does not need any external state up front — the subclass itself picks its initial state in its own constructor.

```csharp
public StateMachineComponent<T>(T routine)
```

Creates a new [StateMachineComponent\<T\>](../../Bang/StateMachines/StateMachineComponent-1.html) wrapping the given, already constructed `routine` instance. Used both by JSON deserialization (to restore a previously-created routine) and by call sites that need to pass constructor arguments to `T`.

**Parameters** \
`routine` [T](../../) — the already-constructed state machine instance to wrap. \

### ⭐ Properties
#### State
```csharp
public virtual string State { get; }
```

Name of the routine (state) the wrapped `T` instance is currently executing. Delegates to `StateMachine.Name`; used for debugging and, when `StateMachine.PersistStateOnSave` is `true`, as the value that gets persisted on save.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### Initialize(World, Entity)
```csharp
public virtual void Initialize(World world, Entity e)
```

Initialize the state machine with the world knowledge. Called before any tick. Forwards to the wrapped `T` instance's own `Initialize`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### OnDestroyed()
```csharp
public virtual void OnDestroyed()
```

Called *before* this component gets replaced, removed or destroyed from the entity. Forwards to the wrapped `T` instance's `OnDestroyed`, which unsubscribes from entity messages and disposes the current routine.

#### Reset()
```csharp
public virtual void Reset()
```

Clean up and reset the state machine. Forwards to `StateMachine.ResetCurrentState`, restarting the wrapped `T` instance's current state from its beginning while discarding any progress made within it. This backs `Entity`/tooling code that needs to force a state machine back to a known starting point (e.g. after restoring one from a save that only persisted the state's name).

#### Subscribe(Action)
```csharp
public virtual void Subscribe(Action notification)
```

Subscribe for notifications on this component. Implements [IModifiableComponent](../../Bang/Components/IModifiableComponent.html) so `Entity` can treat the wrapped state machine consistently with other modifiable components; internally this simply tells the wrapped `T` instance to start listening for entity messages (the `notification` callback itself is not used by the state machine, since state changes are observed through `State` rather than through the modification-notification mechanism).

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Tick(float)
```csharp
public virtual bool Tick(float seconds)
```

Tick a yield operation in the state machine. The next tick will be called according to the returned [WaitKind](../../Bang/StateMachines/WaitKind.html). `seconds` is converted to milliseconds before being forwarded to the wrapped `T` instance's own `Tick`.

**Parameters** \
`seconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — `true` if the state machine should keep being ticked; `false` once it has finished. \

#### Unsubscribe(Action)
```csharp
public virtual void Unsubscribe(Action notification)
```

Stop listening to notifications on this component. Forwards to the wrapped `T` instance to stop listening for entity messages.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡

# IStateMachineComponent

**Namespace:** Bang.StateMachines \
**Assembly:** Bang.dll

```csharp
public abstract IStateMachineComponent : IComponent
```

Component-facing contract for a [StateMachine](../../Bang/StateMachines/StateMachine.html). A [StateMachine](../../Bang/StateMachines/StateMachine.html) subclass is plain C# and knows nothing about being attached to an entity; this interface is what actually gets stored as a component on an [Entity](../../Bang/Entities/Entity.html) (via [StateMachineComponent\<T\>](../../Bang/StateMachines/StateMachineComponent-1.html)) so that the engine can initialize, start and tick it like any other piece of entity state.

Game code should not need to implement this interface directly. Write a [StateMachine](../../Bang/StateMachines/StateMachine.html) subclass and attach it to an entity through [StateMachineComponent\<T\>](../../Bang/StateMachines/StateMachineComponent-1.html) instead (e.g. `entity.SetStateMachine(new StateMachineComponent<MyStateMachine>())`); the engine (and tools such as the editor's asset inspector) then talks to that wrapper purely through this interface, without needing to know the concrete `T`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Properties
#### State
```csharp
public abstract virtual string State { get; }
```

Name of the routine (state) the underlying [StateMachine](../../Bang/StateMachines/StateMachine.html) is currently executing, i.e. the name of the C# method last passed to `StateMachine.State(Func<IEnumerator<Wait>>)`. Not meant to drive gameplay logic directly — this exists so tools and logs can show which state an entity is in, and it is also the value that gets persisted to save data when the owning state machine opts into it.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### Initialize(World, Entity)
```csharp
public abstract void Initialize(World world, Entity e)
```

Gives the state machine a reference to the [World](../../Bang/World.html) it lives in and the [Entity](../../Bang/Entities/Entity.html) it is attached to. Called by the engine once, before the first [Start()](../../Bang/StateMachines/IStateMachineComponent.html#start) or [Tick(float)](../../Bang/StateMachines/IStateMachineComponent.html#tickfloat) call, so the underlying `StateMachine` can use its `World` and `Entity` members from that point on.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### Start()
```csharp
public abstract void Start()
```

Runs any one-time startup logic for the state machine before its first tick. Called by the engine exactly once, after [Initialize(World, Entity)](../../Bang/StateMachines/IStateMachineComponent.html#initializeworld-entity) and before the first [Tick(float)](../../Bang/StateMachines/IStateMachineComponent.html#tickfloat).

#### Tick(float)
```csharp
public abstract bool Tick(float dt)
```

Advances the state machine by one engine update. This resumes the current routine at its last `yield return` point (once any pending [Wait](../../Bang/StateMachines/Wait.html) has elapsed) and runs it until it yields again or finishes. The next tick will be called according to the returned [WaitKind](../../Bang/StateMachines/WaitKind.html).

**Parameters** \
`dt` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — elapsed time, in milliseconds, since the last tick. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — `true` if the state machine should keep being ticked; `false` once it has finished (its routine yielded a stop) and can be discarded. \

#### Reset()
```csharp
public abstract void Reset()
```

Restarts the current state (routine) from its beginning, discarding any progress made within it. Useful for state machines that should re-run a state's setup logic, for example after being reused/pooled or restored from a save that only persisted the state's name.



⚡

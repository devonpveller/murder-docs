# StateWatcherComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct StateWatcherComponent : IModifiableComponent, IComponent
```

This will watch for rule changes based on the blackboard system.

**Intent:** Receive callbacks whenever the state-machine (State) blackboard variables change.

**Use-case:** Added once per world to let systems that depend on state-machine output invalidate cached data the moment any state variable is written.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Methods
#### Subscribe(Action)
```csharp
public virtual void Subscribe(Action notification)
```

Registers a callback that fires whenever the state blackboard values change.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)
```csharp
public virtual void Unsubscribe(Action notification)
```

Removes a previously registered state-blackboard-change callback.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡
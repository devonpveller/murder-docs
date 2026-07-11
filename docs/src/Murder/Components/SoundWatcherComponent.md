# SoundWatcherComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundWatcherComponent : IModifiableComponent, IComponent
```

This will watch for rule changes based on the blackboard system.

**Intent:** Receive callbacks whenever the sound blackboard variables change, so reactive systems can update audio state immediately.

**Use-case:** Added once per world at startup to drive music/ambience transitions; subscribe a callback via `Subscribe` to re-evaluate sound rules whenever the sound blackboard is modified.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Methods
#### Subscribe(Action)
```csharp
public virtual void Subscribe(Action notification)
```

Registers a callback that fires whenever the sound blackboard values change.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)
```csharp
public virtual void Unsubscribe(Action notification)
```

Removes a previously registered sound-blackboard-change callback.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡
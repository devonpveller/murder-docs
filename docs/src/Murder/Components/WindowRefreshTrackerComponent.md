# WindowRefreshTrackerComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct WindowRefreshTrackerComponent : IModifiableComponent, IComponent
```

This will watch for rule changes based on the blackboard system.

**Intent:** Notify subscribed systems whenever the game window is resized or refreshed.

**Use-case:** Added once per scene to let UI layout systems re-calculate element positions and sizes whenever the window dimensions change.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Methods
#### Subscribe(Action)
```csharp
public virtual void Subscribe(Action notification)
```

Registers a callback that fires whenever the window is resized or refreshed.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)
```csharp
public virtual void Unsubscribe(Action notification)
```

Removes a previously registered window-refresh callback.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡
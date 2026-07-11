# IExitSystem

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public abstract IExitSystem : ISystem
```

A system called when the world is shutting down. Use this to release resources, persist
            state, or otherwise clean up before the world and its entities disappear - the same way
            [IStartupSystem](../../Bang/Systems/IStartupSystem.html) is the entry point, this is the guaranteed exit point.

**Implements:** _[ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### Exit(Context)
```csharp
public abstract void Exit(Context context)
```

Called when everything is turning off (this is your last chance). Only active exit
            systems are notified; there is no equivalent "exit" call for systems that were
            deactivated before the world shut down.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡

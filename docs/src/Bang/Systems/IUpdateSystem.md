# IUpdateSystem

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public abstract IUpdateSystem : ISystem
```

A system that consists of a single update call, run once every frame while the system
            is active. This is the workhorse interface for gameplay logic: movement, AI, timers,
            input handling and anything else that needs to tick continuously. Implement this when
            your logic needs to run every frame regardless of a fixed timestep; use
            [IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html) instead when the logic must be decoupled from the
            render frame rate (e.g. physics). [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html) (together with
            [IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html)) is also the default candidate for automatic pausing:
            [World.Pause](../../Bang/World.html) deactivates update systems unless they carry
            [DoNotPauseAttribute](../../Bang/Systems/DoNotPauseAttribute.html) or [OnPauseAttribute](../../Bang/Systems/OnPauseAttribute.html).

**Implements:** _[ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### Update(Context)
```csharp
public abstract void Update(Context context)
```

Update method. Called once every frame for as long as the system is active in the
            [World](../../Bang/World.html), with the `context` already filtered to the
            entities that match this system's [FilterAttribute](../../Bang/Systems/FilterAttribute.html).

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡

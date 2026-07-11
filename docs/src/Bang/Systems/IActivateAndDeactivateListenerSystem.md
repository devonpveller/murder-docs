# IActivateAndDeactivateListenerSystem

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public abstract IActivateAndDeactivateListenerSystem : ISystem
```

This is used for tracking when the system itself - not an entity - gets activated and
            deactivated within the [World](../../Bang/World.html), e.g. via [World.ActivateSystem](../../Bang/World.html)/
            [World.DeactivateSystem](../../Bang/World.html), or automatically as part of
            [World.Pause](../../Bang/World.html)/[World.Resume](../../Bang/World.html) for systems that qualify for pausing
            (see [DoNotPauseAttribute](../../Bang/Systems/DoNotPauseAttribute.html), [OnPauseAttribute](../../Bang/Systems/OnPauseAttribute.html) and
            [IncludeOnPauseAttribute](../../Bang/Systems/IncludeOnPauseAttribute.html)). This is unrelated to [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html),
            whose `OnActivated`/`OnDeactivated` react to *entities* being enabled/disabled - here
            it is the system's own on/off state in the world that is being observed. Implement this when a
            system needs to run setup/teardown logic every time it toggles (not just once, like
            [IStartupSystem](../../Bang/Systems/IStartupSystem.html)/[IExitSystem](../../Bang/Systems/IExitSystem.html)), for example to reset internal state or
            to (de)register from something external whenever it stops or resumes running.

**Implements:** _[ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### OnActivated(Context)
```csharp
public abstract void OnActivated(Context context)
```

Called once the system is activated in the [World](../../Bang/World.html), with the context already
            wired up. For now, this is not called on startup for systems that start active (should we?).

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### OnDeactivated(Context)
```csharp
public abstract void OnDeactivated(Context context)
```

Called once the system is deactivated in the [World](../../Bang/World.html), e.g. via
            [World.DeactivateSystem](../../Bang/World.html) or as part of [World.Pause](../../Bang/World.html).

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡

# IFixedUpdateSystem

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public abstract IFixedUpdateSystem : ISystem
```

A system called at fixed intervals, independent of the render frame rate. Use this
            instead of [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html) for logic that must be deterministic and stable
            regardless of how fast frames are being rendered - the canonical example being physics
            integration, where a variable timestep would make simulation results frame-rate
            dependent. Like [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), systems implementing this interface are
            eligible for automatic deactivation on [World.Pause](../../Bang/World.html) unless they carry
            [DoNotPauseAttribute](../../Bang/Systems/DoNotPauseAttribute.html) or [OnPauseAttribute](../../Bang/Systems/OnPauseAttribute.html).

**Implements:** _[ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### FixedUpdate(Context)
```csharp
public abstract void FixedUpdate(Context context)
```

Update calls that will be called in fixed intervals, with the `context`
            already filtered to the entities that match this system's [FilterAttribute](../../Bang/Systems/FilterAttribute.html).

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡

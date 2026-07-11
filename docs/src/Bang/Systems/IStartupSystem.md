# IStartupSystem

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public abstract IStartupSystem : ISystem
```

A system only called once, the very first time it becomes active in the world. Use this
            for one-time initialization that needs access to a [Context](../../Bang/Contexts/Context.html) - e.g. creating
            singleton entities, caching references, or precomputing data derived from the initial
            world state - instead of doing that work in a constructor, where the rest of the world
            (and other systems' entities) may not exist yet. [World](../../Bang/World.html) tracks internally
            which startup systems have already run, so if a startup system is later deactivated and
            then reactivated (e.g. via [World.ActivateSystem](../../Bang/World.html) or after a
            [World.Pause](../../Bang/World.html)/[World.Resume](../../Bang/World.html) cycle), `Start(Context)`
            will not be called again.

**Implements:** _[ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### Start(Context)
```csharp
public abstract void Start(Context context)
```

This is called before any [IUpdateSystem.Update](../../Bang/Systems/IUpdateSystem.html) or
            [IFixedUpdateSystem.FixedUpdate](../../Bang/Systems/IFixedUpdateSystem.html) call, exactly once for the
            lifetime of the system instance.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡

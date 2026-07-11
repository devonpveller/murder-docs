# TimeScaleSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class TimeScaleSystem : IReactiveSystem, ISystem, IStartupSystem, IExitSystem
```

Aggregates `TimeScaleComponent` values from all active entities (by multiplication) and applies the result to `Game.Instance.TimeScale`.

**Intent:** Allows multiple entities to independently influence global time speed; the effective scale is the product of all active multipliers.

**Use-case:** Attach `TimeScaleComponent` to entities that represent slow-motion or fast-forward effects; removing the component automatically restores the previous speed.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IStartupSystem](../../Bang/Systems/IStartupSystem.html), [IExitSystem](../../Bang/Systems/IExitSystem.html)_

### ⭐ Constructors
```csharp
public TimeScaleSystem()
```

### ⭐ Methods
#### Exit(Context)
```csharp
public virtual void Exit(Context context)
```
Restores the global time scale to 1 when the world exits, preventing the modified scale from leaking into the next scene.
**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Registers new `TimeScaleComponent` values and recalculates the global time scale.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Updates the stored multiplier for modified entities and recalculates the global time scale.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Removes the time-scale multiplier for each removed entity and recalculates the global time scale.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Start(Context)
```csharp
public virtual void Start(Context context)
```

Applies the initial accumulated time scale to `Game.Instance.TimeScale` at world startup.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡
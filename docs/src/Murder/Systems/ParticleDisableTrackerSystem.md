# ParticleDisableTrackerSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class ParticleDisableTrackerSystem : IReactiveSystem, ISystem
```

Reacts to `DisableParticleSystemComponent` being added or removed, activating or deactivating the corresponding particle emitter in the `WorldParticleSystemTracker`.

**Intent:** Allows toggling a particle emitter on and off at runtime through the presence of a component rather than destroying and recreating the entity.

**Use-case:** Add `DisableParticleSystemComponent` to pause a particle effect and remove it to resume; this system handles the emitter state in the tracker automatically.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public ParticleDisableTrackerSystem()
```

### ⭐ Methods
#### OnAdded(World, ImmutableArray<T>)
```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Deactivates the particle emitter in the tracker when `DisableParticleSystemComponent` is added to the entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)
```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

No-op; state changes are handled by add and remove events.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)
```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Re-activates the particle emitter in the tracker when `DisableParticleSystemComponent` is removed from the entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \



⚡
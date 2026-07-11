# ParticleTrackerSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class ParticleTrackerSystem : IReactiveSystem, ISystem
```

Responds to `ParticleSystemComponent` being added, modified, or removed on entities and registers or unregisters them with the `WorldParticleSystemTracker`.

**Intent:** Keeps the particle tracker synchronized with the ECS world so each entity's emitter is managed exactly for the lifetime of its `ParticleSystemComponent`.

**Use-case:** Automatically pairs with `ParticleRendererSystem`; attach `ParticleSystemComponent` to any entity and this system starts and stops the emitter cleanly.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public ParticleTrackerSystem()
```

### ⭐ Methods
#### OnActivated(World, ImmutableArray<T>)
```csharp
public virtual void OnActivated(World world, ImmutableArray<T> entities)
```

Re-registers the entity's emitter with the tracker when the entity is reactivated.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnAdded(World, ImmutableArray<T>)
```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Registers the entity's particle emitter with the world tracker when `ParticleSystemComponent` is added.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnDeactivated(World, ImmutableArray<T>)
```csharp
public virtual void OnDeactivated(World world, ImmutableArray<T> entities)
```

Unregisters the entity's emitter from the tracker when the entity is deactivated.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)
```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Synchronizes updated emitter settings in the world tracker when `ParticleSystemComponent` is modified.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)
```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Unregisters the entity's emitter from the world tracker when `ParticleSystemComponent` is removed.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \



⚡
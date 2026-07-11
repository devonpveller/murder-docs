# IReactiveSystem

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public abstract IReactiveSystem : ISystem
```

A reactive system that reacts to changes of certain components. A reactive system must be
            decorated with [WatchAttribute](../../Bang/Systems/WatchAttribute.html) declaring which component types it wants to be
            notified about, usually together with [FilterAttribute](../../Bang/Systems/FilterAttribute.html) declaring the overall
            entity shape it cares about. Unlike [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html)/[IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html),
            this is not polled every frame: [World](../../Bang/World.html) batches every add, remove and modification
            of a watched component during the frame and delivers them here once, at the end of the frame,
            as an [ImmutableArray\<Entity\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) of affected entities. This
            makes it the right tool for logic that should react to a state transition (a component being
            attached/detached/edited) rather than for logic that needs to run continuously - use
            [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html) for the latter. Note this is unrelated to
            [IActivateAndDeactivateListenerSystem](../../Bang/Systems/IActivateAndDeactivateListenerSystem.html): the `OnActivated`/`OnDeactivated`
            members below fire when watched *entities* are enabled/disabled, whereas
            [IActivateAndDeactivateListenerSystem](../../Bang/Systems/IActivateAndDeactivateListenerSystem.html) fires when the *system itself* is toggled
            on/off within the world.

**Implements:** _[ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### OnAdded(World, ImmutableArray<Entity>)
```csharp
public abstract void OnAdded(World world, ImmutableArray<Entity> entities)
```

This is called at the end of the frame for all entities that were added one of the target.
            components.
            This is not called if the entity died.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<Entity\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<Entity>)
```csharp
public abstract void OnRemoved(World world, ImmutableArray<Entity> entities)
```

This is called at the end of the frame for all entities that removed one of the target.
            components.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<Entity\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<Entity>)
```csharp
public abstract void OnModified(World world, ImmutableArray<Entity> entities)
```

This is called at the end of the frame for all entities that modified one of the target.
            components.
            This is not called if the entity died.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<Entity\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnActivated(World, ImmutableArray<Entity>)
```csharp
public virtual void OnActivated(World world, ImmutableArray<Entity> entities)
```

[Optional] This is called when an entity gets enabled. This fires for entities that
            were reactivated (see `Entity.Activate`), not for the reactive system itself -
            see [IActivateAndDeactivateListenerSystem](../../Bang/Systems/IActivateAndDeactivateListenerSystem.html) for the latter.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<Entity\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnDeactivated(World, ImmutableArray<Entity>)
```csharp
public virtual void OnDeactivated(World world, ImmutableArray<Entity> entities)
```

[Optional] This is called when an entity gets disabled. Called if an entity was
            previously disabled.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<Entity\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnAfterTrigger(World)
```csharp
public virtual void OnAfterTrigger(World world)
```

[Optional] This is called after any of `OnAdded`, `OnRemoved`,
            `OnModified`, `OnActivated` or `OnDeactivated` was
            called for this reactive system during the frame. Useful for batched post-processing
            that should run at most once per frame regardless of how many individual notifications
            were received.

**Parameters** \
`world` [World](../../Bang/World.html) \



⚡

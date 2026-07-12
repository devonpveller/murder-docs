# EventPersistedOnEntityListenerSystem

**Namespace:** Murder.Systems.Effects \
**Assembly:** Murder.dll

```csharp
public class EventPersistedOnEntityListenerSystem : IReactiveSystem, ISystem
```

Stops a persisted event sound (e.g. an ambience loop started by [EventListenerSystem](EventListenerSystem.html)) when its `PlayingPersistedEventComponent` marker is removed or deactivated.

**Intent:** `EventListenerSystem` tags an entity with `PlayingPersistedEventComponent` whenever one of its animation events plays a sound flagged to persist. This system is the counterpart that watches for that marker going away - whether because the entity was deactivated/destroyed or because gameplay code explicitly removed it - and fades out the corresponding sound so it doesn't keep looping forever.

**Use-case:** You normally don't add or remove `PlayingPersistedEventComponent` yourself; it is managed automatically by `EventListenerSystem`. This system exists purely to clean up persisted sounds when that lifecycle ends. It walks the entity's `EventListenerComponent` events looking for ones with a configured sound and calls `SoundServices.Stop` (with a fade-out) for each. Adding or modifying the marker is a no-op here; only removal/deactivation triggers cleanup.

**Implements:** _[IReactiveSystem](../../../Bang/Systems/IReactiveSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public EventPersistedOnEntityListenerSystem()
```

### ⭐ Methods

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

No-op: adding the `PlayingPersistedEventComponent` marker does not require any action from this system.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnDeactivated(World, ImmutableArray<T>)

```csharp
public virtual void OnDeactivated(World world, ImmutableArray<T> entities)
```

Treats deactivation the same as removal: fades out any sounds tied to the entity's event listener, since a deactivated entity should not keep playing a persisted ambience loop.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

No-op: modifying the `PlayingPersistedEventComponent` marker does not require any action from this system.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Fades out every sound referenced by the entity's `EventListenerComponent` events, called when the `PlayingPersistedEventComponent` marker is removed from the entity.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

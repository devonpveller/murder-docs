# ParticleAlphaTrackerSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class ParticleAlphaTrackerSystem : IReactiveSystem, ISystem
```

Watches for changes to `AlphaComponent` on particle-system entities and forwards the new alpha value to the `WorldParticleSystemTracker` so it is applied during rendering.

**Intent:** Bridges entity-level alpha changes to the particle simulation tracker so particle emitters respect per-entity transparency.

**Use-case:** Automatically active alongside `ParticleRendererSystem`; set an `AlphaComponent` on a particle entity to fade the emitter — no extra setup required.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public ParticleAlphaTrackerSystem()
```

### ⭐ Methods

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Delegates to `OnModified` to apply the initial alpha value to the particle tracker.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Reads the entity's `AlphaComponent` and updates the corresponding emitter's alpha in the world particle tracker.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Resets the emitter's alpha to 1 in the particle tracker when `AlphaComponent` is removed from the entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

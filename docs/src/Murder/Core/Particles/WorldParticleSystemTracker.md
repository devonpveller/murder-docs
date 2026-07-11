# WorldParticleSystemTracker

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public class WorldParticleSystemTracker
```

Manages all `ParticleSystemTracker` instances currently active in a `World`, mapping them to their owning entities.

**Intent:** Provide a centralised manager for all particle systems in a game world.

**Use-case:** Retrieve the `WorldParticleSystemTracker` from the world context. Call `Track()` when a particle entity is created, `Untrack()` when it is destroyed, `Step()` each frame to advance all simulations, and `FetchActiveParticleTrackers()` to iterate over them for rendering.

### ⭐ Constructors
```csharp
public WorldParticleSystemTracker(int seed)
```

**Parameters** \
`seed` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods
#### SetAlpha(int, float)
```csharp
public bool SetAlpha(int entityId, float alpha)
```

Set the alpha for a particle system itself according to the <paramref name="entityId" />.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`alpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Synchronize(Entity)
```csharp
public bool Synchronize(Entity particleEntity)
```

Synchronises the tracker's particle definition with the latest asset data for the given entity.

**Parameters** \
`particleEntity` [Entity](../../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Track(Entity)
```csharp
public bool Track(Entity particleEntity)
```

Begins tracking a new particle entity. Returns `false` if the entity is already tracked or has no valid particle asset.

**Parameters** \
`particleEntity` [Entity](../../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FetchActiveParticleTrackers()
```csharp
public ReadOnlySpan<T> FetchActiveParticleTrackers()
```

Fetch all the active particle trackers.

**Returns** \
[ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

#### Activate(int)
```csharp
public void Activate(int id)
```

Marks the particle system associated with entity `id` as active, allowing it to spawn new particles.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Deactivate(int)
```csharp
public void Deactivate(int id)
```

Marks the particle system associated with entity `id` as inactive, pausing new particle spawning.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Step(World)
```csharp
public void Step(World world)
```

Advances all active particle trackers by one frame, stepping their simulations.

**Parameters** \
`world` [World](../../../Bang/World.html) \

#### Untrack(Entity)
```csharp
public void Untrack(Entity particleEntity)
```

Removes the given entity from tracking and returns its slot to the pool.

**Parameters** \
`particleEntity` [Entity](../../../Bang/Entities/Entity.html) \



⚡
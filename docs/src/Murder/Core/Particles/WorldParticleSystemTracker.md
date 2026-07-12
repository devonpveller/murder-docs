# WorldParticleSystemTracker

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public class WorldParticleSystemTracker
```

Manages all `ParticleSystemTracker` instances currently active in a `World`, mapping them to their owning entities.

**Intent:** Provide a centralised manager for all particle systems in a game world.

**Use-case:** A single `WorldParticleSystemTracker` is created and owned by the `ParticleSystemWorldTrackerComponent` on a dedicated singleton entity that `ParticleRendererSystem.Start` adds to the world the first time it runs. Reactive systems call into it as entities with a `ParticleSystemComponent` come and go: `ParticleTrackerSystem` calls `Track()`/`Synchronize()`/`Untrack()` as that component is added, modified, or removed; `ParticleDisableTrackerSystem` calls `Activate()`/`Deactivate()`/`IsTracking()` in response to a `DisableParticleSystemComponent`; `ParticleAlphaTrackerSystem` calls `SetAlpha()` to mirror an entity's `AlphaComponent`; `ParticleRendererSystem` calls `Step()` every update and `FetchActiveParticleTrackers()` every draw.

### ⭐ Constructors

```csharp
public WorldParticleSystemTracker(int seed)
```

Creates the tracker with an initial pool of 32 `ParticleSystemTracker` slots (growing by doubling as needed) and a base random `seed` that is mixed into each tracked system's own seed (and re-incremented on every `Synchronize()` call) so that multiple particle systems spawned from the same asset don't all roll identical random sequences.

**Parameters** \
`seed` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### SetAlpha(int, float)

```csharp
public bool SetAlpha(int entityId, float alpha)
```

Sets the system-level `ParticleSystemTracker.Alpha` for the tracker associated with `entityId`, so an entire particle system fades in and out together (e.g. mirroring the owning entity's `AlphaComponent`, as `ParticleAlphaTrackerSystem` does). Returns `false` and does nothing if `entityId` is not currently tracked.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`alpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Synchronize(Entity)

```csharp
public bool Synchronize(Entity particleEntity)
```

Re-creates the tracker slot for `particleEntity` from its `ParticleSystemComponent`'s current asset, discarding any live particles and re-rolling with an incremented seed. Called by `ParticleTrackerSystem.OnModified` whenever the component changes (e.g. a different particle asset is assigned, or its GUID is edited live in the editor). If the entity is not yet tracked, this falls back to `Track()` instead.

**Parameters** \
`particleEntity` [Entity](../../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Track(Entity)

```csharp
public bool Track(Entity particleEntity)
```

Begins tracking a new particle entity: looks up its `ParticleSystemComponent.Asset` as a `ParticleSystemAsset` and allocates a new `ParticleSystemTracker` for it, marked active so it starts spawning immediately. Returns `false` (and tracks nothing) if the entity already carries a `DisableParticleSystemComponent`, is already tracked, or its asset GUID cannot be resolved. Called by `ParticleTrackerSystem.OnAdded`/`OnActivated` whenever a `ParticleSystemComponent` is added to a live entity, and by `ParticleDisableTrackerSystem.OnRemoved` to start tracking an entity whose `DisableParticleSystemComponent` has just been removed.

**Parameters** \
`particleEntity` [Entity](../../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FetchActiveParticleTrackers()

```csharp
public ReadOnlySpan<T> FetchActiveParticleTrackers()
```

Returns a read-only view over every `ParticleSystemTracker` slot currently in the pool (not just the ones marked "active" for spawning — trackers whose particles are still alive keep rendering even after being deactivated). `ParticleRendererSystem.Draw` iterates this every frame to draw each system's live `ParticleRuntime` instances.

**Returns** \
[ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

#### Activate(int)

```csharp
public void Activate(int id)
```

Marks the particle system associated with entity `id` as active, allowing it to spawn new particles again on the next `Step`. Used by `ParticleDisableTrackerSystem.OnRemoved` when a `DisableParticleSystemComponent` is removed from an entity, resuming emission.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Deactivate(int)

```csharp
public void Deactivate(int id)
```

Marks the particle system associated with entity `id` as inactive: `Step` still advances and pools any already-living particles for that entity, but `allowSpawn` is passed as `false`, so no new ones are created. Used by `ParticleDisableTrackerSystem.OnAdded` when a `DisableParticleSystemComponent` is added, letting an effect wind down naturally instead of stopping abruptly.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### IsTracking(int)

```csharp
public bool IsTracking(int id)
```

Returns whether the particle system for entity `id` is currently marked active (i.e. allowed to spawn new particles) — not merely whether it is tracked at all. `ParticleDisableTrackerSystem.OnRemoved` checks this before re-adding a `Track()` call to avoid double-tracking an entity that was tracked and disabled in the same frame.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Step(World, Rectangle)

```csharp
public void Step(World world, Rectangle cameraArea)
```

Advances every tracked `ParticleSystemTracker` by one frame: for each, resolves the owning entity's current global position and calls `ParticleSystemTracker.Step`, passing whether that entity is in the active set, and passing `null` instead of `cameraArea` when the entity has an `AlwaysInCameraComponent` so it keeps simulating even while off-screen. Called once per update from `ParticleRendererSystem.Update`, with `cameraArea` set to the render camera's safe bounds captured on the previous draw.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`cameraArea` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Untrack(Entity)

```csharp
public void Untrack(Entity particleEntity)
```

Removes the given entity from tracking, returning its `ParticleSystemTracker` slot to the pool (swap-removing it so indices stay dense) and clearing its active-set membership. Called by `ParticleTrackerSystem.OnRemoved`/`OnDeactivated` whenever a `ParticleSystemComponent` is removed or its entity is deactivated — any particles already in flight for that entity simply stop being simulated and drawn.

**Parameters** \
`particleEntity` [Entity](../../../Bang/Entities/Entity.html) \

⚡

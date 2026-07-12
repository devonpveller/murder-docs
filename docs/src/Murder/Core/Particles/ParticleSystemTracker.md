# ParticleSystemTracker

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct ParticleSystemTracker
```

Manages the runtime lifecycle of all live particles for a single particle system instance — spawning, stepping, and pooling.

**Intent:** Act as the per-entity particle simulation engine.

**Use-case:** `ParticleSystemTracker` is created from an `Emitter` and `Particle` definition (usually via a `ParticleSystemAsset`). Call `Step()` each frame to advance the simulation and read `Particles` for rendering.

### ⭐ Constructors

```csharp
public ParticleSystemTracker(Emitter emitter, Particle particle, int seed)
```

**Parameters** \
`emitter` [Emitter](../../../Murder/Core/Particles/Emitter.html) \
`particle` [Particle](../../../Murder/Core/Particles/Particle.html) \
`seed` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Alpha

```csharp
public float Alpha { set; }
```

Write-only opacity multiplier applied to every particle in this system. `WorldParticleSystemTracker.SetAlpha` writes to this from `ParticleAlphaTrackerSystem`, which mirrors the owning entity's `AlphaComponent` (e.g. when the entity fades in/out via a cutscene or dialogue). Each `ParticleRuntime.UpdateAlpha` call is fed this value so the whole system fades together, independent of each particle's own `Particle.Alpha` curve.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### CurrentTime

```csharp
public float CurrentTime { get; }
```

Total elapsed simulation time (in seconds) since this tracker's `Start` was called, advanced by `dt` on every `Step`. Used internally to time bursts/spawns and, alongside `LastEmitterPosition`, exposed for diagnostics such as `WorldParticleSystemTracker.HasParticles`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Emitter

```csharp
public readonly Emitter Emitter;
```

**Returns** \
[Emitter](../../../Murder/Core/Particles/Emitter.html) \

#### LastEmitterPosition

```csharp
public Vector2 LastEmitterPosition { get; }
```

The last position of the emitter, recorded at the top of every `Step` call regardless of whether spawning is allowed. `WorldParticleSystemTracker` does not otherwise track per-tracker positions, so this is the way to recover "where is this particle system currently anchored" (e.g. for debug drawing).

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Particle

```csharp
public readonly Particle Particle;
```

The `Particle` definition (appearance and per-particle physics) this tracker was constructed with. Read by the renderer to look up `Texture`, `SpriteBatch`, `BlendState`, and to evaluate `CalculateColor`/`CalculateScale` for each live `ParticleRuntime`.

**Returns** \
[Particle](../../../Murder/Core/Particles/Particle.html) \

#### Particles

```csharp
public ReadOnlySpan<T> Particles { get; }
```

A read-only view over the currently-live `ParticleRuntime` instances (backed by the tracker's internal pooled array, sliced to the active length). `ParticleRendererSystem` iterates this every draw call to render each particle; nothing outside `Step`/`Start`/`SpawnNewParticlesPerSec` is allowed to mutate the underlying array, which is why this is exposed as a span rather than the array itself.

**Returns** \
[ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

### ⭐ Methods

#### Step(bool, Vector2, Rectangle?, int)

```csharp
public void Step(bool allowSpawn, Vector2 emitterPosition, Rectangle? cameraArea, int id)
```

Advances the simulation by one frame: on the first call it lazily calls `Start`, then steps and pools every live `ParticleRuntime` (applying `Particle.FollowEntityPosition` and the system-level `Alpha` along the way), advances `CurrentTime`, and — unless `cameraArea` is supplied and the emitter's bounding box (`Emitter.BoundingBoxSize()`) does not touch it — spawns new particles via `SpawnNewParticlesPerSec` when `allowSpawn` is `true`. `WorldParticleSystemTracker.Step` calls this once per tracked entity every frame, passing `null` for `cameraArea` when the entity has an `AlwaysInCameraComponent` so it keeps simulating even off-screen.

**Parameters** \
`allowSpawn` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether spawning new entities is allowed, e.g. the entity is not deactivated. \
`emitterPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
Emitter position in game where the particles are fired from. \
`cameraArea` [Rectangle?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
Emitters outside of this area won't step. \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Entity id, used when generating the correct seed for the particle. \

#### Start(Vector2, int)

```csharp
public void Start(Vector2 emitterPosition, int id)
```

Initialises the random seed (mixing in `emitterPosition` and `id` so different instances at different positions don't spawn identically) and resets the timer, then immediately spawns the initial `Emitter.Burst` worth of particles and computes the interval used later for `ParticlesPerSecond` spawning. Called automatically by `Step` the first time it runs on a tracker — game code does not normally need to call this directly.

**Parameters** \
`emitterPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

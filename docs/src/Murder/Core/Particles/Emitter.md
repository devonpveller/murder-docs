# Emitter

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct Emitter
```

Data-driven definition of how a particle system spawns particles — rate, burst count, speed, angle, shape, and pool size.

**Intent:** Describe the spawning behaviour of a particle system.

**Use-case:** Configure an `Emitter` in a `ParticleSystemAsset` to control how many particles spawn per second (`ParticlesPerSecond`), at what angle and speed they fire, and from which shape they originate. Pair it with a `Particle` to define the full system.

### ⭐ Constructors

```csharp
public Emitter()
```

The only constructor. It sets every field to its documented default (a single central point shape, no motion, a pool of 100 particles, scaled time on) so that dropping a bare `new Emitter()` into a `ParticleSystemAsset` produces a valid, if inert, emitter. Because every field carries a default value and `Shape` is `init`-only, editor/agent code builds a customised emitter with an object initializer instead of a parameterised constructor, e.g. `new Emitter() { Shape = someShape }` together with `with`-expressions for the rest (see `WithShape`).

### ⭐ Properties

#### Angle

```csharp
public readonly ParticleValueProperty Angle;
```

The firing angle (in radians) of emitted particles, marked with `[Angle]` so the editor renders it with an angle picker. A random value is sampled per particle and combined with `Speed` inside `ParticleSystemTracker.CreateParticle` to set the particle's initial travel direction (`ParticleRuntime.StartRotation`).

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### Burst

```csharp
public readonly ParticleIntValueProperty Burst;
```

Number of particles to spawn all at once the moment the system starts (`ParticleSystemTracker.Start`). This drives the initial `_currentLength` of a tracker, so a large burst combined with a small `MaxParticlesPool` will silently be capped — `Start` bails out without spawning anything if the rolled burst count exceeds the pool size. Use `Burst` for effects that need an instantaneous puff (explosions, impacts) as opposed to a steady stream, which is controlled by `ParticlesPerSecond` instead.

**Returns** \
[ParticleIntValueProperty](../../../Murder/Core/Particles/ParticleIntValueProperty.html) \

#### MaxParticlesPool

```csharp
public readonly int MaxParticlesPool;
```

Maximum number of simultaneously active particles this emitter can hold. `ParticleSystemTracker` allocates its internal `ParticleRuntime[]` buffer at exactly this size when the tracker is constructed, so it is a hard cap: once that many particles are alive, `SpawnNewParticlesPerSec` stops creating new ones (and, as noted above, an initial `Burst` larger than this value prevents `Start` from spawning anything at all). Set it high enough to cover the peak of `Burst` plus whatever `ParticlesPerSecond` accumulates over a particle's `LifeTime`, but no higher than needed — it is a fixed per-instance allocation.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ParticlesPerSecond

```csharp
public readonly ParticleValueProperty ParticlesPerSecond;
```

Continuous spawn rate: sampled once via `GetRandomValue` at `Start` time to compute the interval between spawns (`1f / ParticlesPerSecond`), and a new particle is created by `ParticleSystemTracker.SpawnNewParticlesPerSec` every time that interval elapses. Use this for effects that emit a steady stream (smoke, fire) as opposed to `Burst`, which fires everything at once.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### ScaledTime

```csharp
public readonly bool ScaledTime;
```

When `true`, the emitter uses the game's scaled delta time, so it respects time-scale (e.g., slow-motion).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Shape

```csharp
public readonly EmitterShape Shape;
```

The geometric shape from which particles are spawned. `ParticleSystemTracker.CreateParticle` samples `Shape.GetRandomPosition(random)` for every new particle to determine its local starting offset from the emitter's world position, and `Emitter.BoundingBoxSize()` uses it to compute the emitter's on-screen bounds for camera culling. Defaults to `EmitterShapeKind.Point` (a single origin) until explicitly set with `WithShape` or an object initializer.

**Returns** \
[EmitterShape](../../../Murder/Core/Particles/EmitterShape.html) \

#### Speed

```csharp
public readonly ParticleValueProperty Speed;
```

Initial launch speed applied to particles when they are emitted. Each particle samples a random value from this property (`GetRandomValue`) and adds it to `Particle.StartVelocity` to form its starting scalar velocity; the direction that velocity travels in is controlled separately by `Angle`.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

### ⭐ Methods

#### WithShape(EmitterShape)

```csharp
public Emitter WithShape(EmitterShape shape)
```

Returns a copy of this emitter with its `Shape` replaced by `shape`.

**Parameters** \
`shape` [EmitterShape](../../../Murder/Core/Particles/EmitterShape.html) \

**Returns** \
[Emitter](../../../Murder/Core/Particles/Emitter.html) \

⚡

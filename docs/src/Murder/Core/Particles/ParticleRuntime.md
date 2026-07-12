# ParticleRuntime

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct ParticleRuntime
```

Runtime state of a single live particle: current position, velocity, rotation, alpha, and lifetime progress.

**Intent:** Store the mutable per-frame state for one active particle instance.

**Use-case:** `ParticleRuntime` instances are managed internally by `ParticleSystemTracker`. Read the `Particles` span on a tracker to iterate over all live particles for custom rendering or post-processing.

### ⭐ Constructors

```csharp
public ParticleRuntime(float startTime, float lifetime, Vector2 position, Vector2 fromPosition, Vector2 gravity, float attraction, float startAlpha, float startVelocity, float startRotation, float startAcceleration, float startFriction, float startRotationSpeed, float fromAlpha, float visualRotation)
```

Builds the runtime state for one newly-spawned particle. This is called exclusively by `ParticleSystemTracker.CreateParticle`, which samples every argument from the owning `Emitter`/`Particle` definitions (e.g. `position` comes from `EmitterShape.GetRandomPosition`, `gravity`/`attraction`/`startAlpha`/etc. come from the corresponding `Particle` properties evaluated at delta `0`). Game and editor code should not normally call this constructor directly — spawn particles by tracking an entity with a `ParticleSystemComponent` instead.

**Parameters** \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`lifetime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`fromPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`gravity` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`attraction` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startAlpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startVelocity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startRotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startAcceleration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startFriction` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startRotationSpeed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`fromAlpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`visualRotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Acceleration

```csharp
public float Acceleration;
```

Current acceleration applied to the particle's velocity each frame.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Alpha

```csharp
public float Alpha;
```

Current opacity of this particle (0–1), blended with the system-level alpha.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Attraction

```csharp
public float Attraction;
```

Strength of the pull towards the centre of the owning particle system, copied from `Particle.Attraction` at spawn time. Read every step: when non-zero, the particle's velocity gets an extra component pointing back at the emitter's current position, scaled by this value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### CurrentVelocity

```csharp
public Vector2 CurrentVelocity { get; private set; }
```

The particle's fully-resolved 2D velocity vector for the current step — its scalar `Velocity` projected along its current travel direction (`StartRotation + Rotation`), plus any attraction pull. Recomputed every `Step` and consumed by `ParticleRendererSystem` when `Particle.RotateWithVelocity` is set, to orient the drawn sprite along the direction of motion.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Delta

```csharp
public float Delta { get; private set; }
```

This is the lifetime of the particle over 0 to 1.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Friction

```csharp
public float Friction;
```

Friction coefficient applied to velocity each frame.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Gravity

```csharp
public Vector2 Gravity;
```

Constant directional force added to velocity each frame.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Lifetime

```csharp
public readonly float Lifetime;
```

Total duration (in seconds) this particle will live.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Position

```csharp
public Vector2 Position { get; }
```

Current world-space position (`_fromPosition + _localPosition`).

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Rotation

```csharp
public float Rotation;
```

Current rotation angle in radians.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### RotationSpeed

```csharp
public float RotationSpeed;
```

Angular velocity in radians per second.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### StartRotation

```csharp
public float StartRotation;
```

The initial rotation angle assigned at spawn time.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Velocity

```csharp
public float Velocity;
```

Current scalar speed of this particle along its direction of travel.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### VisualRotation

```csharp
public float VisualRotation;
```

Cosmetic-only rotation offset (degrees), copied from `Particle.VisualRotation` at spawn time. `ParticleRendererSystem` adds it to the draw rotation on top of `StartRotation + Rotation` (and `RotateWithVelocity`'s facing), without influencing the particle's actual velocity or trajectory.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### Step(Particle&, float, Vector2, float)

```csharp
public void Step(Particle& particle, float currentTime, Vector2 particleSystemCenter, float dt)
```

Advances this particle's simulation by one time step `dt`. Called once per live particle, per frame, from `ParticleSystemTracker.Step`. Recomputes `Delta` from elapsed time versus `Lifetime`, re-samples `Alpha`/`Acceleration`/`Friction`/`Rotation` from `particle` at the new `Delta`, integrates `Velocity` (applying acceleration then friction), derives `CurrentVelocity` from the resulting direction, adds the attraction pull towards `particleSystemCenter` when `Attraction` is non-zero, and finally advances the particle's local position by `CurrentVelocity * dt + Gravity * dt`.

**Parameters** \
`particle` [Particle&](../../../Murder/Core/Particles/Particle.html) \
Value on the particle based on the asset. \
`currentTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
Current time that the particle system exists. \
`particleSystemCenter` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
The center of the particle system, used for attraction. \
`dt` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
Delta time since the last Step call. \

#### UpdateAlpha(float)

```csharp
public void UpdateAlpha(float alpha)
```

Multiplies the particle's alpha by the system-level `alpha` value.

**Parameters** \
`alpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### UpdateFromPosition(Vector2)

```csharp
public void UpdateFromPosition(Vector2 from)
```

Updates the emitter origin used when `Particle.FollowEntityPosition` is `true`.

**Parameters** \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

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

```csharp
public Emitter(int maxParticles, EmitterShape shape, ParticleValueProperty angle, ParticleValueProperty particlesPerSecond, ParticleIntValueProperty burst, ParticleValueProperty speed)
```

**Parameters** \
`maxParticles` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`shape` [EmitterShape](../../../Murder/Core/Particles/EmitterShape.html) \
`angle` [ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \
`particlesPerSecond` [ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \
`burst` [ParticleIntValueProperty](../../../Murder/Core/Particles/ParticleIntValueProperty.html) \
`speed` [ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

### ⭐ Properties
#### Angle
```csharp
public readonly ParticleValueProperty Angle;
```

The firing angle (in radians) of emitted particles. Supports constant values, ranges, and curves.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \
#### Burst
```csharp
public readonly ParticleIntValueProperty Burst;
```

Number of particles to spawn all at once when the emitter triggers a burst.

**Returns** \
[ParticleIntValueProperty](../../../Murder/Core/Particles/ParticleIntValueProperty.html) \
#### MaxParticlesPool
```csharp
public readonly int MaxParticlesPool;
```

Maximum number of simultaneously active particles this emitter can hold.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### ParticlesPerSecond
```csharp
public readonly ParticleValueProperty ParticlesPerSecond;
```

Continuous spawn rate in particles per second.

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

The geometric shape from which particles are spawned.

**Returns** \
[EmitterShape](../../../Murder/Core/Particles/EmitterShape.html) \
#### Speed
```csharp
public readonly ParticleValueProperty Speed;
```

Initial launch speed applied to particles when they are emitted.

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
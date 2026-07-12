# Particle

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct Particle
```

Data-driven definition of per-particle appearance and behaviour: texture, lifetime, color, scale, velocity, gravity, rotation, and blend state.

**Intent:** Describe how each individual particle in a system looks and moves.

**Use-case:** Configure a `Particle` in a `ParticleSystemAsset` alongside an `Emitter`. Set `LifeTime`, `Colors`, `Scale`, `Alpha`, `StartVelocity`, and `Texture` to craft the desired visual effect.

### ⭐ Constructors

```csharp
public Particle()
```

The only constructor. It leaves every field at its documented default (white color, `Vector2.One` scale, empty/zero value properties, alpha-blended, not following the entity) so a bare `new Particle()` is a valid, if visually inert, particle definition. Because every field carries a default and `Texture`/`Rotation` are `init`-only, callers customise a particle with an object initializer or the `WithTexture`/`WithRotation` `with`-expression helpers rather than a parameterised constructor.

### ⭐ Properties

#### Acceleration

```csharp
public readonly ParticleValueProperty Acceleration;
```

Rate at which the particle's velocity changes over its lifetime.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### Alpha

```csharp
public readonly ParticleValueProperty Alpha;
```

Opacity of the particle over its lifetime (0–1).

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### Attraction

```csharp
public readonly ParticleValueProperty Attraction;
```

Strength of a constant pull towards the centre of the particle system (the emitter's current position). Each `ParticleRuntime.Step` computes the normalized direction from the particle back to the emitter and adds `direction * Attraction * dt` to the particle's velocity, so a positive value makes particles curve back inward (e.g. a "gathering" or vortex-like effect) while `0` (the default) disables the pull entirely.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### BlendState

```csharp
public readonly MurderBlendState BlendState;
```

The blend mode used by `ParticleRendererSystem` when drawing particles of this type — for example `AlphaBlend` (the default) for normal translucent particles or an additive mode for glowing effects like sparks and fire. Applies uniformly to every rendering path (`Point`, `Rectangle`, `Circle`, `Asset`, `Texture`) supported by `ParticleTexture.Kind`.

**Returns** \
[MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \

#### Colors

```csharp
public readonly ImmutableArray<T> Colors;
```

Color gradient sampled over the particle's lifetime. Linearly interpolated between entries.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FollowEntityPosition

```csharp
public readonly bool FollowEntityPosition;
```

When `true`, the particle's world position tracks the emitter entity's position each frame.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Friction

```csharp
public readonly ParticleValueProperty Friction;
```

Friction coefficient (0–1) applied each frame to slow the particle down.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### Gravity

```csharp
public readonly ParticleVectorValueProperty Gravity;
```

Constant directional velocity applied to every particle each frame (world-space gravity).

**Returns** \
[ParticleVectorValueProperty](../../../Murder/Core/Particles/ParticleVectorValueProperty.html) \

#### LifeTime

```csharp
public readonly ParticleValueProperty LifeTime;
```

Duration in seconds that each particle lives.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### RotateWithVelocity

```csharp
public readonly bool RotateWithVelocity;
```

When `true`, the particle's visual rotation aligns with its current velocity direction.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Rotation

```csharp
public readonly ParticleValueProperty Rotation;
```

Initial rotation angle (radians) assigned when the particle is spawned.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### RotationSpeed

```csharp
public readonly ParticleValueProperty RotationSpeed;
```

Angular velocity (radians per second) applied to the particle's rotation each frame.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### Scale

```csharp
public readonly ImmutableArray<T> Scale;
```

Scale keyframes sampled over the particle's lifetime. Linearly interpolated between entries.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### SortOffset

```csharp
public readonly float SortOffset;
```

Additional Y offset applied when sorting this particle relative to other rendered entities.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SpriteBatch

```csharp
public readonly int SpriteBatch;
```

Index of the sprite batch pass used when rendering particles of this type.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### StartVelocity

```csharp
public readonly ParticleValueProperty StartVelocity;
```

Initial scalar velocity of the particle, added on top of the emitter's launch speed.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

#### Texture

```csharp
public readonly ParticleTexture Texture;
```

The texture configuration that defines how each particle is drawn.

**Returns** \
[ParticleTexture](../../../Murder/Core/Particles/ParticleTexture.html) \

#### VisualRotation

```csharp
public readonly ParticleValueProperty VisualRotation;
```

An additional rotation (in degrees, clamped to -180..180 in the editor via `[Slider]`) added purely for the visual sort/draw pass, layered on top of the particle's physical `Rotation`/`RotationSpeed`. `ParticleRendererSystem` converts it to radians and adds it to the draw rotation after computing `RotateWithVelocity`, which is useful for cosmetic spin (e.g. tumbling debris) that shouldn't affect the particle's actual trajectory.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

### ⭐ Methods

#### CalculateColor(float)

```csharp
public Color CalculateColor(float delta)
```

Evaluates the `Colors` gradient at lifetime progress `delta` (0 = just spawned, 1 = about to die), linearly interpolating between adjacent color entries. Returns opaque white if `Colors` is empty, or the single entry directly if only one color is set. Called by `ParticleRendererSystem` every frame for every live particle, multiplied by the particle's current `Alpha`.

**Parameters** \
`delta` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
Delta from 0 to 1. \

**Returns** \
[Color](../../../Murder/Core/Graphics/Color.html) \

#### WithRotation(float)

```csharp
public Particle WithRotation(float rotation)
```

Returns a copy of this particle with `Rotation` set to `rotation` (radians).

**Parameters** \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Particle](../../../Murder/Core/Particles/Particle.html) \

#### WithTexture(ParticleTexture)

```csharp
public Particle WithTexture(ParticleTexture texture)
```

Returns a copy of this particle with `Texture` replaced by `texture`.

**Parameters** \
`texture` [ParticleTexture](../../../Murder/Core/Particles/ParticleTexture.html) \

**Returns** \
[Particle](../../../Murder/Core/Particles/Particle.html) \

#### CalculateScale(float)

```csharp
public Vector2 CalculateScale(float delta)
```

Evaluates the `Scale` keyframes at lifetime progress `delta` (0 = just spawned, 1 = about to die), linearly interpolating between adjacent entries. Returns `Vector2.One` if `Scale` is empty, or the single entry directly if only one is set. Called by `ParticleRendererSystem` every frame to size each live particle's draw quad — e.g. use multiple entries to make a particle grow then shrink over its life.

**Parameters** \
`delta` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
Delta from 0 to 1. \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

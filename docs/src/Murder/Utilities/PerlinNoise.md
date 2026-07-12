# PerlinNoise

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class PerlinNoise
```

A standalone, static implementation of Ken Perlin's classic 3D gradient noise, using a fixed permutation table so results are deterministic across platforms and runs (there is no seed to configure).

**Intent:** This is separate from the simplex/value noise families in [NoiseHelper](../../Murder/Utilities/NoiseHelper.html); it exists specifically to back `RandomExtensions.SmoothRandom(float, float)`, which flattens the 3D sample down to a smooth 1D signal by holding two of the three coordinates fixed.

**Use-case:** Prefer `RandomExtensions.SmoothRandom` for gameplay code that wants a smoothly-varying "random" curve over a single changing value (e.g. glitchy text jitter in `PixelFont`); call `Noise` directly only if you need the raw 3D sample.

### ⭐ Methods

#### Noise(float, float, float)

```csharp
public float Noise(float x, float y, float z)
```

Samples classic 3D Perlin gradient noise at the given coordinate and normalizes the result to `[0, 1]` (the raw Perlin output is roughly `[-1, 1]`).

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — X input coordinate. \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Y input coordinate. \
`z` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Z input coordinate. \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — A smoothly-varying pseudorandom value normalized to approximately `[0, 1]`. \

⚡

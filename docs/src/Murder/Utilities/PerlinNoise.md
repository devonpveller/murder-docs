# PerlinNoise

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class PerlinNoise
```

A static implementation of classic Perlin noise for generating smooth pseudo-random values.

**Intent:** Provides classic 3D Perlin noise sampling for procedural content generation.

**Use-case:** Call `Noise(x, y, z)` to sample a smooth noise value at a 3D coordinate; useful for terrain height maps, texture variation, or oscillating animation offsets.

### ⭐ Methods
#### Noise(float, float, float)
```csharp
public float Noise(float x, float y, float z)
```

Returns a Perlin noise value in approximately [-1, 1] for the given 3D sample coordinate.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`z` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \



⚡
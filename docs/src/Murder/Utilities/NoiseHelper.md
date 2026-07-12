# NoiseHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed class NoiseHelper
```

Collects several unrelated pseudo-random noise generators — Carmody's and Gustavson's simplex noise, plus a lightweight value-noise pair — behind one static entry point.

**Intent:** All state (permutation tables, seed) is shared across every call, so setting `Seed` once affects every subsequent noise sample from this class. This gives callers a single place to reach for deterministic, spatially-coherent pseudo-randomness instead of hand-rolling noise math per feature.

**Use-case:** Every member of this class is `static`; there is no need to keep an instance around even though the class is not itself declared `static`. Use `Value2D`/`Value1D` for cheap, high-frequency sampling (e.g. picking a floor-tile sprite variant per grid cell in `TilemapAndFloorRenderSystem`/`FloorWithBatchOptimizationRenderSystem`, or jittering an entity's animation start time in `AgentSpriteSystem`/`SpriteRenderDebugSystem`), and `CarmodyNoise`/`GustavsonNoise` when you need genuine simplex noise (e.g. `TilesetAsset` uses `GustavsonNoise` to pick a randomized-but-stable auto-tile frame per cell).

### ⭐ Constructors

```csharp
public NoiseHelper()
```

The implicit parameterless constructor. Since every member of this class is `static`, there is normally no reason to construct an instance — call the static members directly (e.g. `NoiseHelper.Value2D(x, y)`).

### ⭐ Properties

#### Seed

```csharp
public static int Seed { set; }
```

Write-only. Sets the seed used by every noise family in this class. Assigning this property immediately reseeds Carmody's hash table and recomputes Gustavson's permutation table, so all subsequent calls to `CarmodyNoise` and `GustavsonNoise` (using their default `doReseed`/`doRecalculate` arguments) become deterministic and reproducible for the same seed value. Leave unset (or pass `false` for `doReseed`/`doRecalculate` on individual calls) to keep noise varying between runs.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### CarmodyNoise(float, float, float, bool, bool)

```csharp
public float CarmodyNoise(float x, float y, float z, bool doReseed, bool doNormalize)
```

Carmody's implementation of a 3D Simplex Noise generator. By default (`doReseed: true`) each call reseeds the internal hash table from a fresh `Random`, so successive calls are **not** deterministic relative to each other unless you either pass `doReseed: false` after the first call or set `Seed` beforehand.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — X position. \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Y position. \
`z` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Z position. \
`doReseed` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — Force reseeding of the permutation table before sampling. \
`doNormalize` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — Normalize the output to `[0, 1]` instead of the default `[-1, 1]`-ish range. \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — A value in the range of about `[-1, 1]` (or `[0, 1]` if `doNormalize` is `true`). \

#### GustavsonNoise(float, float, bool, bool)

```csharp
public float GustavsonNoise(float xin, float yin, bool doRecalculate, bool doNormalize)
```

Gustavson's implementation of a 2D Simplex Noise generator. Used by `TilesetAsset.DrawTile` (with `doRecalculate: false, doNormalize: true`) to derive a stable, cell-coordinate-based pseudo-random index into a tile's available frames, so the same cell always renders the same auto-tile variant.

**Parameters** \
`xin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — X position. \
`yin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Y position. \
`doRecalculate` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — Force recalculation of the permutation table (can also be done by setting `NoiseHelper.Seed`). \
`doNormalize` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — Normalize the output to `[0, 1]` instead of `[-1, 1]`. \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — A value in the range of about `[-1, 1]` (or `[0, 1]` if `doNormalize` is `true`). \

#### GustavsonNoise(float, float, float, bool, bool)

```csharp
public float GustavsonNoise(float xin, float yin, float zin, bool doRecalculate, bool doNormalize)
```

Gustavson's implementation of a 3D Simplex Noise generator.

**Parameters** \
`xin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — X position. \
`yin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Y position. \
`zin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Z position. \
`doRecalculate` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — Force recalculation of the permutation table (can also be done by setting `NoiseHelper.Seed`). \
`doNormalize` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — Whether the output should be normalized to `[0, 1]`. \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — A value in the range of about `[-1, 1]` (or `[0, 1]` if `doNormalize` is `true`). \

#### Normalize(float, float, float)

```csharp
public float Normalize(float value, float min, float max)
```

Normalizes a float from a known `[min, max]` range to `[0, 1]`. Used internally by the noise generators to remap their raw simplex output; also usable directly on any bounded value.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — The float to be normalized. \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — The minimum value in the range. \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — The maximum value in the range. \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### NormalizeSigned(float, float, float)

```csharp
public float NormalizeSigned(float value, float min, float max)
```

Normalizes a float from a known `[min, max]` range to `[-1, 1]`. Used internally by `CarmodyNoise` to remap its raw output when `doNormalize` is `false`.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — The float to be normalized. \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — The minimum value in the range. \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — The maximum value in the range. \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Value2D(float, float, float)

```csharp
public float Value2D(float x, float y, float frequency)
```

Smooth 2D value noise in the range `[0, 1]`, deterministic and tileable. Cheaper than the simplex generators above (no gradient dot products, just four lattice lookups and a bilinear/smoothstep blend), which makes it well suited for high-frequency, per-call sampling such as picking a floor-tile variant per grid cell (`TilemapAndFloorRenderSystem`, `FloorWithBatchOptimizationRenderSystem`).

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — X input coordinate. \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Y input coordinate. \
`frequency` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Grid frequency (higher = more variation over the same input range); defaults to `1f`. \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Smoothed pseudorandom float between 0 and 1. \

#### Value1D(float, float)

```csharp
public float Value1D(float x, float frequency)
```

Smooth 1D value noise in the range `[0, 1]`, deterministic and tileable. Used to jitter a per-entity value (such as an animation start offset in `AgentSpriteSystem`/`SpriteRenderDebugSystem`) so entities don't all animate perfectly in sync, while still being stable across frames for the same input.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Input coordinate. \
`frequency` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Grid frequency (higher = more variation); defaults to `1f`. \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Smoothed pseudorandom float between 0 and 1. \

⚡

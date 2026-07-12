# FloatRange

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct FloatRange
```

An inclusive `[Start, End]` interval of float values.

**Intent:** A min-max pair of floats designed to be dropped directly on a component field and edited in the editor as a slider (see the `[Slider(0, 1)]` attribute on both fields), then sampled at runtime with `GetRandom` or interpolated with `Lerp`. `TweenComponent.Time`, for example, uses a `FloatRange` to represent the start/end progress window over which a tween is applied.

**Use-case:** Pass a `FloatRange` to any system that needs to draw a random value or interpolate between two bounds — randomized spawn delays, tween progress windows, particle emitter lifetimes, and similar min/max gameplay tuning values.

### ⭐ Constructors

```csharp
public FloatRange(float start, float end)
```

Creates a float range with the given inclusive lower and upper bounds.

**Parameters** \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`end` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### End

```csharp
public readonly float End;
```

Inclusive upper bound of the range. Rendered in the editor as a 0-1 slider by default (see the `[Slider(0, 1)]` attribute), though nothing prevents constructing a range outside that window in code.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Start

```csharp
public readonly float Start;
```

Inclusive lower bound of the range. Rendered in the editor as a 0-1 slider by default.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### Contains(float)

```csharp
public bool Contains(float v)
```

Returns `true` when `v` falls within `[Start, End]` (inclusive). Useful for checking whether a sampled or elapsed value has entered/left the range, e.g. testing a tween's current progress against its configured window.

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetRandom()

```csharp
public float GetRandom()
```

Draws a random value within `[Start, End]` using the shared, deterministic `Game.Random` instance. Prefer this over passing your own `Random` unless a call site specifically needs an independent, seedable stream (e.g. for replay determinism isolated from the rest of the game's randomness).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetRandom(Random)

```csharp
public float GetRandom(Random random)
```

Draws a random value within `[Start, End]` using the supplied `random` source.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Lerp(float)

```csharp
public float Lerp(float progress)
```

Linearly interpolates from `Start` to `End` by `progress` (0 = `Start`, 1 = `End`). Use this instead of `GetRandom` when a value should scale smoothly and deterministically across the range rather than being sampled randomly — for example, driving a tween's actual value from its normalized progress.

**Parameters** \
`progress` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

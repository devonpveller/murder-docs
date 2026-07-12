# FadeScreenComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeScreenComponent : IComponent
```

Encapsulates the parameters for a full-screen fade effect (in, out, flash, or buffered out).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Carries every parameter a fade rendering system would need (color/texture, duration, direction, sorting, target batch) as a single component, decoupled from any particular renderer. It is marked `[DoNotPersistOnSave]` since a fade is a transient runtime effect that should never be written into a save file. Note that the base Murder engine itself does not ship a system that reads this component — it is created purely as data by `EffectsServices`, and a game (or its own render/UI layer) is expected to provide the system that consumes it and actually draws the overlay.

**Use-case:** Created by `EffectsServices.FadeIn`/`FadeOut` rather than constructed directly, so that `StartedTime` is stamped with the correct game time and any previous `FadeScreenComponent` entities are cleaned up first; `FadeIn` also honors `Game.Instance.IsSkippingDeltaTimeOnUpdate` by not creating the fade at all when the game is fast-forwarding.

### ⭐ Constructors

```csharp
public FadeScreenComponent(FadeType fade, float startedTime, float duration, Color color, string customTexture, float sorting, int bufferFrames)
```

Creates the fade parameters for a full-screen fade effect. `duration` is clamped to a minimum of `0.1` seconds.

**Parameters** \
`fade` [FadeType](../../Murder/Components/FadeType.html) \
`startedTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`customTexture` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bufferFrames` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### BufferFrames

```csharp
public readonly int BufferFrames { get; init; }
```

Number of extra frames to hold at the peak of the fade before reversing; used by `FadeType.OutBuffer` to avoid one-frame flickers.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Color

```csharp
public readonly Color Color;
```

Color of the fade overlay (typically black for a normal fade-to-black).

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### CustomTexture

```csharp
public readonly string CustomTexture;
```

Optional path to a texture used instead of a solid color for the fade overlay (e.g., a vignette or wipe texture).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Duration

```csharp
public readonly float Duration;
```

Length of the fade effect in seconds; clamped to a minimum of `0.1`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Fade

```csharp
public readonly FadeType Fade;
```

The type of fade effect to apply (in, out, flash, or buffered out).

**Returns** \
[FadeType](../../Murder/Components/FadeType.html) \

#### Sorting

```csharp
public readonly float Sorting;
```

Sort order for the fade overlay within its render batch; higher values draw on top.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### StartedTime

```csharp
public readonly float StartedTime { get; init; }
```

The game time (in seconds) at which the fade began; used to compute interpolation progress.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TargetBatch

```csharp
public readonly int? TargetBatch { get; init; }
```

Optional sprite batch id to draw the fade overlay into; when `null`, the consuming fade system chooses a default batch. `EffectsServices.FadeIn` allows callers to override this per-call.

**Returns** \
[int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

⚡

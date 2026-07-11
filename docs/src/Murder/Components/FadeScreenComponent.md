# FadeScreenComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeScreenComponent : IComponent
```

Drives a full-screen fade effect managed by `FadeScreenSystem`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Encapsulates all parameters needed for a screen fade (in, out, flash, or buffered) so the render system can apply it without additional context.

**Use-case:** Added by `EffectsServices.FadeIn`/`FadeOut` helpers; do not typically create manually — use the service methods instead to ensure `StartedTime` is set correctly.

### ⭐ Constructors
```csharp
public FadeScreenComponent(FadeType fade, float startedTime, float duration, Color color, string customTexture, float sorting, int bufferFrames)
```

Fades the screen using the FadeScreenSystem. Duration will be a minimum of 0.1

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
public int BufferFrames { get; public set; }
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
public float StartedTime { get; public set; }
```

The game time (in seconds) at which the fade began; used to compute interpolation progress.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡
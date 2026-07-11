# RenderTargets

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
sealed enum RenderTargets : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Enumerates the standard render targets managed by a `RenderContext` and available for sampling or inspection.

**Intent:** Provides a stable, named handle for each pipeline render target so callers can retrieve the underlying texture without knowing internal field names.

**Use-case:** Pass a `RenderTargets` value to `RenderContext.GetRenderTargetFromEnum()` to obtain the corresponding `Texture2D`, for example to feed the UI layer into a custom shader.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### FinalTarget
```csharp
public static const RenderTargets FinalTarget;
```

The screen-resolution buffer containing the fully composited frame ready to be blitted to the display.

**Returns** \
[RenderTargets](../../../Murder/Core/Graphics/RenderTargets.html) \
#### MainBufferTarget
```csharp
public static const RenderTargets MainBufferTarget;
```

The game-resolution buffer where all gameplay sprites are drawn before post-processing.

**Returns** \
[RenderTargets](../../../Murder/Core/Graphics/RenderTargets.html) \
#### UiTarget
```csharp
public static const RenderTargets UiTarget;
```

The render target that holds the UI layer drawn above the gameplay buffer.

**Returns** \
[RenderTargets](../../../Murder/Core/Graphics/RenderTargets.html) \


⚡
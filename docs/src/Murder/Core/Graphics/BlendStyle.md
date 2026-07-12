# BlendStyle

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum BlendStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Controls how a sprite's color is combined with the framebuffer when rendering.

**Intent:** Selects the per-pixel blending formula applied by the sprite shader, independently of the `BlendState` (which is GPU-level).

**Use-case:** Set `DrawInfo.BlendMode` to change a sprite's blending at draw time; use `Wash` to tint a sprite with a solid color, `Color` for full color-replace, and `Normal` for standard alpha blending.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Color

```csharp
public static const BlendStyle Color;
```

Replaces the sprite's RGB channels entirely with the tint color, preserving the original alpha.

**Returns** \
[BlendStyle](../../../Murder/Core/Graphics/BlendStyle.html) \

#### Normal

```csharp
public static const BlendStyle Normal;
```

Standard alpha-blending; the sprite texture colors are modulated by the tint color.

**Returns** \
[BlendStyle](../../../Murder/Core/Graphics/BlendStyle.html) \

#### Wash

```csharp
public static const BlendStyle Wash;
```

Blends the tint color over the sprite proportionally to the tint's alpha, effectively "washing" the sprite with a color.

**Returns** \
[BlendStyle](../../../Murder/Core/Graphics/BlendStyle.html) \

⚡

# ColorHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class ColorHelper
```

Extension methods for converting between color representations and generating colors from HSV or hex values.

**Intent:** Provides color conversion and generation utilities used by the editor and gameplay code.

**Use-case:** Use `ToVector4Color` to parse hex colors from editor inputs, `MultiplyAlpha` for premultiplied-alpha rendering, and `ColorFromIndex`/`ColorFromHSV` to generate visually distinct debug or palette colors.

### ⭐ Methods
#### MultiplyAlpha(Color)
```csharp
public Color MultiplyAlpha(Color color)
```

Multiplies the RGB channels by the alpha channel to produce a premultiplied-alpha color suitable for direct alpha-blended rendering.

**Parameters** \
`color` [Color](https://docs.monogame.net/api/Microsoft.Xna.Framework.Color.html) \

**Returns** \
[Color](https://docs.monogame.net/api/Microsoft.Xna.Framework.Color.html) \

#### ToVector4Color(string)
```csharp
public Vector4 ToVector4Color(string hex)
```

Parses a string <paramref name="hex" /> to [Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0).

**Parameters** \
`hex` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \
\



⚡
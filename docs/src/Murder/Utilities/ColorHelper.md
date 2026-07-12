# ColorHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class ColorHelper
```

Extension and static helpers for converting between color representations (hex strings, HSV, premultiplied alpha) and for generating visually-distinct colors, used by both the editor and gameplay code.

**Intent:** Provides color conversion and generation utilities used by the editor and gameplay code.

**Use-case:** Use `ToVector4Color` to parse hex colors from editor inputs, `MultiplyAlpha` for premultiplied-alpha rendering (the format MonoGame's default blend state expects), and `ColorFromIndex`/`ColorFromHSV` to generate visually distinct debug/palette colors — `ImGuiHelpers` in the editor uses `ColorFromIndex` to assign a stable, distinct color per index (e.g. per-layer or per-category swatches).

### ⭐ Methods

#### ColorFromHSV(float, float, float)

```csharp
public Color ColorFromHSV(float h, float s, float v)
```

Converts an HSV color to RGB. `h` (hue) is in `[0, 360]`; `s` (saturation) and `v` (value) are in `[0, 1]`. This is the standard HSV→RGB conversion; used internally by `ColorFromIndex` and directly wherever code needs to reason about color in hue/saturation/value terms (e.g. color pickers, generating a palette by sweeping hue).

**Parameters** \
`h` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`s` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Color](https://docs.monogame.net/api/Microsoft.Xna.Framework.Color.html) \

#### ColorFromIndex(int, int, float, float)

```csharp
public Color ColorFromIndex(int index, int total, float saturation, float value)
```

Generates a unique, visually distinct color based on `index` out of `total` possible indices, by spacing hues evenly around the color wheel (`index / total` of a full 360° turn) and converting via `ColorFromHSV`. `saturation`/`value` default to 0.6/0.9. Use to assign a consistent, easily-distinguishable debug color to each item in a small, known-size collection (e.g. one color per editor layer or per gizmo).

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`total` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`saturation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Color](https://docs.monogame.net/api/Microsoft.Xna.Framework.Color.html) \

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

Parses a hex color string such as `"#ff5545"` (via `System.Drawing.ColorTranslator`) into a `Vector4` with components in `[0, 1]` and alpha fixed at 1. Used to convert hex color values from asset/editor input into a shader- and math-friendly `Vector4`.

**Parameters** \
`hex` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

⚡

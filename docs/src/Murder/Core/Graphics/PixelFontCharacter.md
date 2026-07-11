# PixelFontCharacter

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class PixelFontCharacter
```

Stores per-glyph metrics for a single character in a bitmap font.

**Intent:** Represents one character's position in the atlas texture along with its draw offsets, advance width, and optional kerning pairs.

**Use-case:** Used internally by `PixelFontSize` during text layout; inspect directly when building custom text rendering or measuring individual glyphs.

### ⭐ Constructors
```csharp
public PixelFontCharacter()
```

```csharp
public PixelFontCharacter(int character, Rectangle rectangle, int xOffset, int yOffset, int xAdvance)
```

**Parameters** \
`character` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`rectangle` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`xOffset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`yOffset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`xAdvance` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Character
```csharp
public int Character;
```

Unicode codepoint of this glyph.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Glyph
```csharp
public Rectangle Glyph;
```

Source rectangle within the atlas texture that contains this glyph's bitmap.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### Kerning
```csharp
public ImmutableDictionary<TKey, TValue> Kerning;
```

Optional per-following-character horizontal adjustments applied after this glyph; keys are the next character's codepoint and values are pixel offsets.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### Page
```csharp
public int Page;
```

Index of the atlas texture page that contains this glyph.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### XAdvance
```csharp
public int XAdvance;
```

Horizontal advance in pixels — how far the cursor moves right after drawing this glyph.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### XOffset
```csharp
public int XOffset;
```

Horizontal draw offset in pixels applied relative to the current cursor position before rendering the glyph.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### YOffset
```csharp
public int YOffset;
```

Vertical draw offset in pixels applied relative to the baseline before rendering the glyph.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
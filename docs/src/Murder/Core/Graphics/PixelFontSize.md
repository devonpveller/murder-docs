# PixelFontSize

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class PixelFontSize
```

Holds the glyph data, atlas textures, and line metrics for one point-size variant of a `PixelFont`.

**Intent:** Contains everything needed to measure and render text at a specific bitmap font size — the character dictionary, texture pages, and vertical metrics.

**Use-case:** Accessed through `PixelFont.PixelFontSize`; pass it to `TextDataServices.GetOrCreateText()` to produce a cached layout, or call `Draw()` to render directly.

### ⭐ Constructors

```csharp
public PixelFontSize()
```

### ⭐ Properties

#### BaseLine

```csharp
public float BaseLine;
```

Y coordinate of the font baseline within a line, in pixels, measured from the top of the line.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Characters

```csharp
public Dictionary<TKey, TValue> Characters;
```

Lookup table mapping Unicode codepoints to their `PixelFontCharacter` glyph data (atlas rect, offsets, advance, kerning).

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### Index

```csharp
public int Index { get; init; }
```

Index of the font that this belongs to.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### LineHeight

```csharp
public int LineHeight;
```

Total pixel height per text line, encompassing ascenders, glyphs, and descenders.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Offset

```csharp
public Point Offset;
```

Additional pixel offset applied globally when drawing all glyphs in this font size.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Textures

```csharp
public MurderTexture[] Textures;
```

Array of atlas texture pages that contain this font size's glyph bitmaps.

**Returns** \
[MurderTexture[]](../../../Murder/Core/Graphics/MurderTexture.html) \

### ⭐ Methods

#### HeightOf(ReadOnlySpan<T>)

```csharp
public float HeightOf(ReadOnlySpan<T> text)
```

Returns the total pixel height required to render the given (possibly multi-line) text, computed as the number of lines times `LineHeight`.

**Parameters** \
`text` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetCharacterWidth(char)

```csharp
public float GetCharacterWidth(char c)
```

Returns the horizontal advance, in pixels, of a single character in this font size, or `0` if this font size has no glyph for it. A `0` result for a non-space character generally means the character is missing from the font asset; `MurderFontServices.IsValidCharacter` uses this (via `PixelFont.GetCharacterWidth`) to validate that user-entered characters can actually be rendered.

**Parameters** \
`c` [char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### WidthToNextLine(ReadOnlySpan<T>, int, bool)

```csharp
public float WidthToNextLine(ReadOnlySpan<T> text, int start, bool trimWhitespace)
```

Returns the pixel width of the text from `start` up to the first newline or end of the span, optionally trimming trailing whitespace.

**Parameters** \
`text` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
`start` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`trimWhitespace` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Draw(RuntimeTextData, Batch2D, Vector2, Vector2, Vector2, int, float, Color, T?, T?, bool)

```csharp
public Point Draw(RuntimeTextData data, Batch2D spriteBatch, Vector2 position, Vector2 origin, Vector2 scale, int visibleCharacters, float sort, Color color, T? strokeColor, T? shadowColor, bool debugBox)
```

Renders pre-parsed `RuntimeTextData` to the batch with optional stroke, shadow, and a visible-character limit for typewriter effects. Returns the bottom-right pixel extent of the drawn text.

**Parameters** \
`data` [RuntimeTextData](../../../Murder/Core/Graphics/RuntimeTextData.html) \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`visibleCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`strokeColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`shadowColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`debugBox` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Draw(string, Batch2D, Vector2, Vector2, Vector2, int, float, Color, T?, T?, int, bool)

```csharp
public Point Draw(string text, Batch2D spriteBatch, Vector2 position, Vector2 origin, Vector2 scale, int visibleCharacters, float sort, Color color, T? strokeColor, T? shadowColor, int maxWidth, bool debugBox)
```

Draw a text with pixel font. If <paramref name="maxWidth" /> is specified, this will automatically wrap the text.

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`visibleCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`strokeColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`shadowColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`debugBox` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### DrawSimple(string, Batch2D, Vector2, Vector2, Vector2, float, Color, T?, T?, bool)

```csharp
public Point DrawSimple(string text, Batch2D spriteBatch, Vector2 position, Vector2 justify, Vector2 scale, float sort, Color color, T? strokeColor, T? shadowColor, bool debugBox)
```

Renders a plain string without word-wrap or cached layout; intended for single-line or pre-formatted text.

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`justify` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`strokeColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`shadowColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`debugBox` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### AutoNewline(string, int)

```csharp
public string AutoNewline(string text, int width)
```

Inserts newline characters into `text` so that no line exceeds `width` pixels, splitting on word boundaries where possible.

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### WrapString(ReadOnlySpan<T>, int, float)

```csharp
public string WrapString(ReadOnlySpan<T> text, int maxWidth, float scale)
```

Wraps the input span into a string by inserting newlines so that no line exceeds `maxWidth` pixels at the given scale.

**Parameters** \
`text` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`scale` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Measure(string)

```csharp
public Vector2 Measure(string text)
```

Returns the pixel width and height of the bounding box required to render the given text.

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

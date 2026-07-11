# PixelFont

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class PixelFont
```

Bitmap font that manages one or more point-size variants loaded from a `FontAsset`, and provides text measurement and rendering.

**Intent:** Provides text rendering at a specific bitmap font by dispatching measurement and draw calls to the appropriate `PixelFontSize` variant.

**Use-case:** Obtain a `PixelFont` from `Game.Data.GetFont()` and call `Draw()` to render pixel-accurate text to a `Batch2D` layer, or `GetLineWidth()` to measure a line before rendering.

### ⭐ Constructors
```csharp
public PixelFont(FontAsset asset)
```

**Parameters** \
`asset` [FontAsset](../../../Murder/Assets/Graphics/FontAsset.html) \

### ⭐ Properties
#### Index
```csharp
public int Index;
```

Identifier index of this font within the game's loaded font registry.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### LineHeight
```csharp
public int LineHeight { get; }
```

Height of a single line in pixels for the current font size, including ascenders and descenders.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### PixelFontSize
```csharp
public PixelFontSize PixelFontSize { get; }
```

The loaded size data containing glyph metrics, atlas textures, and line measurements.

**Returns** \
[PixelFontSize](../../../Murder/Core/Graphics/PixelFontSize.html) \
### ⭐ Methods
#### GetLineWidth(ReadOnlySpan<T>)
```csharp
public float GetLineWidth(ReadOnlySpan<T> text)
```

Returns the pixel width of a single line of text without applying wrapping or newline handling.

**Parameters** \
`text` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Draw(Batch2D, RuntimeTextData, Vector2, Vector2, Vector2, float, Color, T?, T?, int, bool)
```csharp
public Point Draw(Batch2D spriteBatch, RuntimeTextData data, Vector2 position, Vector2 alignment, Vector2 scale, float sort, Color color, T? strokeColor, T? shadowColor, int visibleCharacters, bool debugBox)
```

Renders pre-parsed `RuntimeTextData` to the batch with optional stroke, shadow, and a visible-character limit for typewriter effects.

**Parameters** \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`data` [RuntimeTextData](../../../Murder/Core/Graphics/RuntimeTextData.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`alignment` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`strokeColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`shadowColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`visibleCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`debugBox` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Draw(Batch2D, string, Vector2, Vector2, Vector2, float, Color, T?, T?, int, int, bool)
```csharp
public Point Draw(Batch2D spriteBatch, string text, Vector2 position, Vector2 alignment, Vector2 scale, float sort, Color color, T? strokeColor, T? shadowColor, int maxWidth, int visibleCharacters, bool debugBox)
```

Renders a string to the batch, automatically wrapping at `maxWidth` and supporting stroke, shadow, and typewriter reveal.

**Parameters** \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`alignment` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`strokeColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`shadowColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`visibleCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`debugBox` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### DrawSimple(Batch2D, string, Vector2, Vector2, Vector2, float, Color, T?, T?, bool)
```csharp
public Point DrawSimple(Batch2D spriteBatch, string text, Vector2 position, Vector2 alignment, Vector2 scale, float sort, Color color, T? strokeColor, T? shadowColor, bool debugBox)
```

Renders a plain string without cached layout or word-wrap; intended for single-line or already-wrapped text.

**Parameters** \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`alignment` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`strokeColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`shadowColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`debugBox` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Escape(string)
```csharp
public string Escape(string text)
```

Strips or escapes any special markup tags (e.g. wave, color, shake) from the input string, returning plain text.

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Preload()
```csharp
public void Preload()
```

Loads all glyph atlas textures into GPU memory ahead of time to prevent hitches on first draw.

⚡
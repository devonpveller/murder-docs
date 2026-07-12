# MurderFontServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class MurderFontServices
```

Provides utilities for measuring rendered text and resolving text-embedded icons using the engine's built-in pixel font system.

**Intent:** Allows game code to query the pixel width/height of a string, validate whether individual characters exist in the active font, and look up icon portraits referenced by text, all before (or instead of) actually rendering the text.

**Use-case:** Call `GetLineWidth`/`MeasureText` before calling `RenderServices.DrawText` to centre a label, fit text inside a fixed-width panel, or truncate overflowing text. Call `IsValidCharacter` when validating free-form player input (e.g. save file names) against the default font's glyph set. Call `TryGetIconForText` when resolving inline icon codes (e.g. `<icon=jump>`) embedded in localized dialogue text.

### ⭐ Methods

#### GetLineHeight(int, string, int)

```csharp
public static float GetLineHeight(int font, string text, int width = -1)
```

Returns the total rendered height of `text` in pixels when drawn with `font`, wrapping at `width` pixels if positive (or a single line if `width` is `-1`). Internally builds/reuses a cached `RuntimeTextData` via `TextDataServices.GetOrCreateText` to account for line wraps.

**Parameters** \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetLineHeight(RuntimeTextData)

```csharp
public static float GetLineHeight(RuntimeTextData text)
```

Returns the rendered pixel height of an already-computed `RuntimeTextData` block, using its font's `PixelFontSize.HeightOf`. Prefer this overload when you already hold a `RuntimeTextData` (e.g. from `TextDataServices`) to avoid recomputing it.

**Parameters** \
`text` [RuntimeTextData](../../Murder/Core/Graphics/RuntimeTextData.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetLineWidth(int, string)

```csharp
public static float GetLineWidth(int font, string text)
```

Returns the pixel width of `text` when rendered with the font identified by its integer index, using a cached `RuntimeTextData`.

**Parameters** \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetLineWidth(MurderFonts, string)

```csharp
public static float GetLineWidth(this MurderFonts font, string text)
```

Extension-method overload of `GetLineWidth(int, string)` that accepts a `MurderFonts` enum value instead of a raw font index.

**Parameters** \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetLineWidth(MurderFonts, ReadOnlySpan\<char\>)

```csharp
public static float GetLineWidth(this MurderFonts font, ReadOnlySpan<char> text)
```

Zero-allocation overload of `GetLineWidth` that measures a `ReadOnlySpan<char>` directly against the font's glyph metrics, bypassing the `RuntimeTextData` cache. Prefer this in hot paths (e.g. per-frame layout) where `text` is already a span and allocating a string/cache entry would be wasteful.

**Parameters** \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [ReadOnlySpan\<char\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### IsValidCharacter(char)

```csharp
public static bool IsValidCharacter(char c)
```

Returns whether `c` has a non-zero glyph width in the engine's default font (`Game.Data.DefaultFont`), i.e. whether it can actually be rendered. Useful for filtering or validating player-typed text (such as save names) against unsupported characters before it is displayed.

**Parameters** \
`c` [char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### MeasureText(int, string, bool)

```csharp
public static Point MeasureText(int font, string text, bool cultureInvariant = false)
```

Returns the bounding size (width and line height) of `text` as it would be rendered with `font`, packed into a `Point`. Set `cultureInvariant` to `true` to force culture-invariant text shaping (e.g. for text that should not be affected by the current OS locale, such as internal debug labels).

**Parameters** \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`cultureInvariant` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### TryGetIconForText(string)

```csharp
public static Portrait? TryGetIconForText(string id)
```

Looks up an inline icon `Portrait` for the identifier `id` in the game's `TextIconsAsset` (`Game.Profile.TextIcons`). Returns `null` if no `TextIconsAsset` is configured or `id` does not resolve to a known icon. Used to render small inline icons (e.g. button prompts) embedded inside otherwise-plain dialogue or UI text.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Portrait?](../../Murder/Core/Portrait.html) \

⚡

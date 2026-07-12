# TextDataServices

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public static class TextDataServices
```

Static service that parses raw text strings into `RuntimeTextData` layouts, processing markup tags and caching results to avoid repeated work.

**Intent:** Acts as the single entry point for converting a raw dialogue or UI string (possibly containing rich-text markup like colors, `<wave>`, `<shake/>`, `<speed=.3/>`, pauses, and inline icons) into display-ready `RuntimeTextData`, with an internal cache keyed on text content, font, and wrap width so repeated calls with the same arguments are cheap after the first.

**Use-case:** Call `GetOrCreateText()` before every `PixelFont.Draw()` call (which does this internally); results are automatically cached so repeated renders of the same string are nearly free. `IsPonctuation()`/`TrimSpaces()`/`EscapeRegex()` and `SPECIAL_BREAK_WORD_CHARACTER` are lower-level helpers reused by `PixelFont` and `StringHelper` when working with already-processed text.

### ⭐ Properties

#### SPECIAL_BREAK_WORD_CHARACTER

```csharp
public const char SPECIAL_BREAK_WORD_CHARACTER;
```

Sentinel character (the ASCII bell character, `'\a'`) inserted in place of a `<bp>` markup tag to mark a manual word-wrap breakpoint. `PixelFont` treats this character as an invisible, zero-width preferred line-break position instead of printing it.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

### ⭐ Methods

#### EscapeRegex()

```csharp
public Regex EscapeRegex()
```

Regex matching color markup tags (`<c=...>` and `</c>`), used to strip color tags out of a string without processing them, e.g. by `PixelFont.Escape()` when producing a plain-text version of dialogue.

**Returns** \
[Regex](https://learn.microsoft.com/en-us/dotnet/api/System.Text.RegularExpressions.Regex?view=net-7.0) \

#### GetOrCreateText(PixelFontSize, string, TextSettings)

```csharp
public RuntimeTextData GetOrCreateText(PixelFontSize font, string text, TextSettings settings)
```

Parses `text` into a `RuntimeTextData`, resolving all supported markup tags (colors, wave, fear, shake, glitch, speed, pauses, inline icons, "new" markers) into per-character `RuntimeLetterProperties`, collapsing/normalizing whitespace and newlines, and applying word-wrap according to `settings`. Reuses a cached result if the same text, font, and wrap width were parsed before.

**Parameters** \
`font` [PixelFontSize](../../../Murder/Core/Graphics/PixelFontSize.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`settings` [TextSettings](../../../Murder/Core/Graphics/TextSettings.html) \

**Returns** \
[RuntimeTextData](../../../Murder/Core/Graphics/RuntimeTextData.html) \

#### GetOrCreateText(int, string, TextSettings)

```csharp
public RuntimeTextData GetOrCreateText(int fontId, string text, TextSettings settings)
```

Looks up the font registered under `fontId` and parses `text` into a `RuntimeTextData` for it, reusing a cached result if the same text/font/width were parsed before.

**Parameters** \
`fontId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`settings` [TextSettings](../../../Murder/Core/Graphics/TextSettings.html) \

**Returns** \
[RuntimeTextData](../../../Murder/Core/Graphics/RuntimeTextData.html) \

#### IsPonctuation(char)

```csharp
public bool IsPonctuation(char c)
```

Returns whether `c` is one of the punctuation characters (Western and full-width/Japanese variants) that the word-wrapper and glitch effect treat specially, e.g. allowing a line break right after it, or excluding it from the glitch animation.

**Parameters** \
`c` [char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsPonctuationToIgnorePreviousPause(char)

```csharp
public bool IsPonctuationToIgnorePreviousPause(char c)
```

Returns whether the character immediately following an inserted pause is punctuation (or a quote) that should cause that pause to be skipped, e.g. so a `|` pause marker right before a `!` doesn't produce an awkward double-pause when the exclamation mark itself already implies one.

**Parameters** \
`c` [char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TrimSpaces()

```csharp
public Regex TrimSpaces()
```

Regex matching two or more consecutive spaces, used to collapse repeated whitespace down to a single space during text parsing. Exposed publicly so other string-processing helpers (e.g. `StringHelper`) can reuse the same rule.

**Returns** \
[Regex](https://learn.microsoft.com/en-us/dotnet/api/System.Text.RegularExpressions.Regex?view=net-7.0) \

⚡

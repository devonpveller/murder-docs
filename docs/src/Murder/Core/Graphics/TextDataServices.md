# TextDataServices

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public static class TextDataServices
```

Static service that parses raw text strings into `RuntimeTextData` layouts, processing markup tags and caching results to avoid repeated work.

**Intent:** Acts as the single entry point for converting a raw dialogue or UI string into display-ready `RuntimeTextData`, with an internal LRU cache keyed on text content, font, and wrap width.

**Use-case:** Call `GetOrCreateText()` before every `PixelFont.Draw()` call; results are automatically cached so repeated renders of the same string are nearly free.

### ⭐ Methods
#### EscapeRegex()
```csharp
public Regex EscapeRegex()
```

Returns the compiled regex used to strip or escape special markup tags from raw text strings.

**Returns** \
[Regex](https://learn.microsoft.com/en-us/dotnet/api/System.Text.RegularExpressions.Regex?view=net-7.0) \

#### GetOrCreateText(PixelFontSize, string, TextSettings)
```csharp
public RuntimeTextData GetOrCreateText(PixelFontSize font, string text, TextSettings settings)
```

Returns cached or newly computed `RuntimeTextData` for the given font size, text content, and layout settings.

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

Looks up the font by its registered index and returns cached or newly computed `RuntimeTextData` for the given text and settings.

**Parameters** \
`fontId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`settings` [TextSettings](../../../Murder/Core/Graphics/TextSettings.html) \

**Returns** \
[RuntimeTextData](../../../Murder/Core/Graphics/RuntimeTextData.html) \



⚡
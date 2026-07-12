# ScreenshotFeedbackData

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public readonly struct ScreenshotFeedbackData
```

Bundles a captured screenshot's encoded file data together with the live `Texture` it was captured from. Declared as a nested type of [FeedbackServices](../../Murder/Services/FeedbackServices.html).

**Intent:** Keeps the PNG bytes ready for upload (`File`) alongside the `Texture` reference so it can be disposed once the feedback submission finishes, since screenshot textures are otherwise not owned/tracked by anything else.

**Use-case:** Returned by `FeedbackServices.TryGetGameplayScreenshot`/`TryGetScreenshot`; pass the resulting values through `FeedbackData.Screenshots` to `SendSaveDataFeedbackAsync`, which attaches `File` to the outgoing request and disposes `Texture` once the submission completes.

### ⭐ Constructors

```csharp
public ScreenshotFeedbackData(string identifier, FileWrapper file, Texture texture)
```

Wraps a captured screenshot's multipart field name (`identifier`), its encoded PNG bytes (`file`), and the source `Texture` (`texture`) that will need disposing after the request completes.

**Parameters** \
`identifier` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`file` [FileWrapper](../../Murder/Services/FileWrapper.html) \
`texture` [Texture](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture.html) \

### ⭐ Properties

#### File

```csharp
public readonly FileWrapper File;
```

The PNG-encoded screenshot data and filename, ready to be attached to a feedback request.

**Returns** \
[FileWrapper](../../Murder/Services/FileWrapper.html) \

#### Identifier

```csharp
public readonly string Identifier;
```

The multipart form field name this screenshot is submitted under (e.g. `"g_screenshot"` or `"screenshot"`), distinguishing gameplay-only vs. full-window captures on the server side.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Texture

```csharp
public readonly Texture Texture;
```

The live texture the screenshot was captured from. `FeedbackServices.SendSaveDataFeedbackAsync` disposes this once the feedback submission completes, so callers should not dispose it themselves after handing it off.

**Returns** \
[Texture](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture.html) \

⚡

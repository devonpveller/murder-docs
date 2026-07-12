# FeedbackServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class FeedbackServices
```

Provides methods for capturing diagnostic data (save files, screenshots, logs) and submitting it as player/tester feedback to a remote HTTP endpoint.

**Intent:** Abstracts the whole "collect a bug report" pipeline — zipping the active or a temporary save, grabbing a screenshot, attaching the current and any previous crash log, and posting all of it as multipart form data — so a feedback UI or crash handler only needs to call one or two high-level methods instead of assembling the payload itself.

**Use-case:** Call `SendSaveDataFeedbackAsync` from an in-game feedback form to bundle the player's message, a fresh copy of their save, and any pending screenshots and send them to `Game.FeedbackUrl`. Call `TryGetGameplayScreenshot`/`TryGetScreenshot` beforehand (on the main thread, since they need the graphics device) to capture the images to attach. For fully custom payloads (e.g. a crash reporter that doesn't go through the save-feedback flow), build a `RawFeedbackData` directly and call `SendFeedbackAsync`.

### ⭐ Properties

#### FeedbackUrlFail

```csharp
public static bool FeedbackUrlFail;
```

Set to `true` the first time a feedback POST fails with an `HttpRequestException` (e.g. the endpoint is unreachable). Once set, `SendFeedbackAsync` short-circuits and returns `false` immediately without attempting further network calls, avoiding repeated failed requests (and their associated timeouts) for the rest of the session.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Methods

#### CreateTemporarySaveAndZipAsync()

```csharp
public static Task<FileWrapper?> CreateTemporarySaveAndZipAsync()
```

Creates a temporary copy of the active save (via `Game.Data.CreateTemporarySaveAsync`) in a fresh temp directory, zips it, and returns the archive as a [FileWrapper](../../Murder/Services/FileWrapper.html). Returns `null` if there is no active save or the temporary save couldn't be created. This is preferred over zipping the live save directory directly (see the private `TryZipActiveSaveAsync` counterpart) because it avoids capturing a save file that could still be mid-write.

**Returns** \
[Task\<FileWrapper?\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task-1?view=net-7.0) \

#### SendSaveDataFeedbackAsync(FeedbackData)

```csharp
public static Task<bool> SendSaveDataFeedbackAsync(FeedbackData data)
```

The main entry point for a player feedback submission. Attaches a freshly zipped copy of the current save (`CreateTemporarySaveAndZipAsync`), the live save directory if present (`TryZipActiveSaveAsync`), and every screenshot in `data.Screenshots`, along with the previous crash log (if any) and the current session log, then posts everything via `SendFeedbackAsync`. Disposes the screenshot textures in `data.Screenshots` once the request completes, regardless of success. Returns whether the submission succeeded.

**Parameters** \
`data` [FeedbackData](../../Murder/Services/FeedbackData.html) \

**Returns** \
[Task\<bool\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task-1?view=net-7.0) \

#### SendFeedbackAsync(RawFeedbackData)

```csharp
public static Task<bool> SendFeedbackAsync(RawFeedbackData data)
```

Posts `data` as `multipart/form-data` to `data.Url`, including title/description/crash log/log/version fields, a `DEBUG`-vs-release `Environment` marker, and every file in `data.Files`. Returns `false` without attempting the request if `data.Url` is empty or `FeedbackUrlFail` is already `true`. On an `HttpRequestException`, sets `FeedbackUrlFail = true`, logs a warning, and returns `false`; on success, logs the response body and returns `true`. This is the low-level method that `SendSaveDataFeedbackAsync` builds on — use it directly when you need to send a feedback payload that isn't a save-data bug report.

**Parameters** \
`data` [RawFeedbackData](../../Murder/Services/RawFeedbackData.html) \

**Returns** \
[Task\<bool\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task-1?view=net-7.0) \

#### TryGetGameplayScreenshot(string)

```csharp
public static ScreenshotFeedbackData? TryGetGameplayScreenshot(string name)
```

Captures a screenshot of just the gameplay render target (via `RenderServices.CreateGameplayScreenshot`), encodes it as PNG, and wraps it in a [ScreenshotFeedbackData](../../Murder/Services/ScreenshotFeedbackData.html) tagged with identifier `"g_screenshot"`. Returns `null` if the screenshot couldn't be captured. Must be called on the main thread since it needs the graphics device.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ScreenshotFeedbackData?](../../Murder/Services/ScreenshotFeedbackData.html) \

#### TryGetScreenshot(string)

```csharp
public static ScreenshotFeedbackData? TryGetScreenshot(string name)
```

Captures a full-window screenshot (via `RenderServices.CreateScreenshot`, including UI rather than just gameplay), encodes it as PNG, and wraps it in a `ScreenshotFeedbackData` tagged with identifier `"screenshot"`. Returns `null` if the screenshot couldn't be captured. Must be called on the main thread since it needs the graphics device.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ScreenshotFeedbackData?](../../Murder/Services/ScreenshotFeedbackData.html) \

#### GenerateFunnyName(int)

```csharp
public static string GenerateFunnyName(int seed)
```

Deterministically generates a whimsical, pronounceable placeholder name (alternating consonant/vowel syllables, 3–8 characters long) from `seed`, using a `Random` seeded with that value. Used to label feedback submissions with a stable, anonymous "computer name" (`seed` is typically `data.MachineId`) instead of exposing real machine identifiers.

**Parameters** \
`seed` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

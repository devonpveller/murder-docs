# FeedbackServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class FeedbackServices
```

Provides asynchronous methods for sending player feedback and diagnostic data to a remote endpoint.

**Intent:** Abstracts the HTTP submission of player feedback, optionally bundling the current game log or save data.

**Use-case:** Call `SendFeedbackAsync` from an in-game feedback form to transmit the player's message (and optionally a zipped save file) to a developer-specified URL for bug reporting or playtesting feedback.

### ⭐ Methods
#### SendFeedbackAsync(string, bool)
```csharp
public Task SendFeedbackAsync(string message, bool sendLog)
```
Sends a feedback message to the configured endpoint, optionally attaching the game log.

**Parameters** \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`sendLog` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### SendFeedbackAsync(string, string, FileWrapper[])
```csharp
public Task SendFeedbackAsync(string url, string message, FileWrapper[] files)
```
Sends a feedback message to `url` with an array of file attachments.

**Parameters** \
`url` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`files` [FileWrapper[]](../../Murder/Services/FileWrapper.html) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### SendSaveDataFeedbackAsync(string)
```csharp
public Task<TResult> SendSaveDataFeedbackAsync(string message)
```
Sends a feedback message with the player's current save data attached as a zip file.

**Parameters** \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Task\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task-1?view=net-7.0) \

#### TryZipActiveSaveAsync()
```csharp
public Task<TResult> TryZipActiveSaveAsync()
```
Attempts to zip the active save directory and returns the archive as a `FileWrapper`, or `null` if no save is active.

**Returns** \
[Task\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task-1?view=net-7.0) \



⚡
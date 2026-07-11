# FileWrapper

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
sealed struct FileWrapper
```

A lightweight container pairing raw file bytes with a filename, used for attaching files to feedback submissions.

**Intent:** Bundles binary file content with its name for transmission over HTTP.

**Use-case:** Populate and pass to `FeedbackServices.SendFeedbackAsync` when attaching a save archive, screenshot, or log file to a feedback report.

### ⭐ Constructors
```csharp
public FileWrapper(Byte[] bytes, string name)
```

**Parameters** \
`bytes` [byte[]](https://learn.microsoft.com/en-us/dotnet/api/System.Byte?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Bytes
```csharp
public readonly Byte[] Bytes;
```
The raw binary content of the file.

**Returns** \
[byte[]](https://learn.microsoft.com/en-us/dotnet/api/System.Byte?view=net-7.0) \
#### Name
```csharp
public readonly string Name;
```
The filename (with extension) used when submitting this file as an attachment.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡
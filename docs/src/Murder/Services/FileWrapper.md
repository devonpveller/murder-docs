# FileWrapper

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public readonly struct FileWrapper
```

A lightweight container pairing raw file bytes with a filename. Declared as a nested type of [FeedbackServices](../../Murder/Services/FeedbackServices.html).

**Intent:** Bundles binary file content with its display/upload name so it can be passed around and attached to an HTTP request without separately tracking the two pieces of data.

**Use-case:** Produced internally by `FeedbackServices` (`CreateTemporarySaveAndZipAsync`, the screenshot helpers) and consumed by `SendFeedbackAsync`/`SendSaveDataFeedbackAsync`, which attach each `FileWrapper`'s `Bytes` to the outgoing multipart request under `Name`. You generally won't construct one directly unless you're extending the feedback pipeline with a new kind of attachment.

### ⭐ Constructors

```csharp
public FileWrapper(byte[] bytes, string name)
```

Wraps `bytes` as the file's raw content and `name` as the filename that will be sent to the server (including its extension, e.g. `"save.zip"` or `"screenshot.png"`).

**Parameters** \
`bytes` [byte[]](https://learn.microsoft.com/en-us/dotnet/api/System.Byte?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Bytes

```csharp
public readonly byte[] Bytes;
```

The raw binary content of the file, as sent verbatim in the HTTP request body.

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

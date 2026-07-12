# RawFeedbackData

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public readonly struct RawFeedbackData
```

The fully-assembled payload that [FeedbackServices](../../Murder/Services/FeedbackServices.html)`.SendFeedbackAsync` posts as multipart form data to a feedback endpoint. Declared as a nested type of `FeedbackServices`.

**Intent:** Represents everything a feedback/crash-report HTTP request needs — target URL, human-readable title/description, crash and session logs, version, and file attachments — as a single immutable value, decoupling the low-level "send this to the server" logic (`SendFeedbackAsync`) from the higher-level "build this from a player's feedback form" logic (`SendSaveDataFeedbackAsync`).

**Use-case:** `SendSaveDataFeedbackAsync` builds one of these automatically from a `FeedbackData`. Construct one directly when you need to submit a report that doesn't go through that flow — e.g. a crash handler that wants to attach a callstack and a previous crash log without bundling save data.

### ⭐ Constructors

```csharp
public RawFeedbackData(string url)
```

Creates a `RawFeedbackData` targeting `url`, with every other field defaulted to an empty string (or an empty file list). Use object-initializer syntax to set `Title`, `Description`, `Files`, and the other fields after construction.

**Parameters** \
`url` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Callstack

```csharp
public string Callstack { get; init; }
```

An optional callstack string to include with the report, typically populated by a crash handler.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### CrashLog

```csharp
public string CrashLog { get; init; }
```

The contents of the previous session's crash log file, if one existed, included so the server has context on any prior crash leading up to this report.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Description

```csharp
public string Description { get; init; }
```

The main body text of the report, sent as the `Description` form field.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Files

```csharp
public IEnumerable<(string name, FileWrapper file)> Files { get; init; }
```

The set of file attachments to include in the multipart request, each paired with the form field name it should be sent under (e.g. `"save"`, `"c_save"`, or a screenshot identifier).

**Returns** \
[IEnumerable\<ValueTuple\<string, FileWrapper\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### Log

```csharp
public string Log { get; init; }
```

The current session's log contents (from `GameLogger.GetCurrentLog`), included to give the server visibility into what happened leading up to the report.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Title

```csharp
public string Title { get; init; }
```

The report's title, sent as the `Title` form field — typically a short summary combined with an anonymized machine identifier.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Url

```csharp
public readonly string Url;
```

The feedback endpoint the request is posted to. `SendFeedbackAsync` refuses to send anything if this is empty.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Version

```csharp
public string Version { get; init; }
```

The game version string included with the report, for triaging against a specific build.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

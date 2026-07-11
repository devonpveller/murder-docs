# DebugServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class DebugServices
```

Development utilities for timing, logging, and runtime debug rendering.

**Intent:** Provides helpers used during development for measuring performance and capturing diagnostic output.

**Use-case:** Use `StopwatchStart`/`StopwatchStop` to measure code segments in milliseconds; use `SaveLogAsync` to persist the current session log to disk for reporting.

### ⭐ Properties
#### DebugPreviewImage
```csharp
public static Texture2D DebugPreviewImage;
```
A texture that can be set at runtime and used as a preview/debug overlay image.

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
### ⭐ Methods
#### StopwatchStart()
```csharp
public DateTime StopwatchStart()
```
Records the current time as the start of a stopwatch measurement and returns it.

**Returns** \
[DateTime](https://learn.microsoft.com/en-us/dotnet/api/System.DateTime?view=net-7.0) \

#### StopwatchStop()
```csharp
public float StopwatchStop()
```
Computes the elapsed time in milliseconds since the last `StopwatchStart` call, logs it, and returns the value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SaveLogAsync(string)
```csharp
public Task SaveLogAsync(string fullpath)
```
Appends all currently buffered game log lines to the file at `fullpath`.

**Parameters** \
`fullpath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \



⚡
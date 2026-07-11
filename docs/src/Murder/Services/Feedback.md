# Feedback

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
sealed struct Feedback
```

A data packet that bundles a player message, a signature, the current game version, and an optional log for submission to a feedback endpoint.

**Intent:** Represents a single structured feedback submission, ready to be serialised and sent to a remote server.

**Use-case:** Constructed automatically by `FeedbackServices`; inspect `Signature` for server-side verification or `Log` to see the captured game log attached to the report.

### ⭐ Constructors
```csharp
public Feedback(string message, string secretKey, bool saveLog)
```

**Parameters** \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`secretKey` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`saveLog` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### Log
```csharp
public readonly string Log;
```
The game log snapshot captured at the time the feedback was created (empty when `saveLog` is `false`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Message
```csharp
public readonly string Message;
```
The human-readable message entered by the player.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Signature
```csharp
public readonly string Signature;
```
An HMAC or similar signature derived from the message and secret key, used by the server to verify authenticity.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Time
```csharp
public readonly DateTime Time;
```
The UTC timestamp when this feedback packet was created.

**Returns** \
[DateTime](https://learn.microsoft.com/en-us/dotnet/api/System.DateTime?view=net-7.0) \
#### Version
```csharp
public readonly float Version;
```
The game version number at the time the feedback was submitted.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡
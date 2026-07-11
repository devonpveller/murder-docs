# UpdateTimeTracker

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class UpdateTimeTracker
```

Track the latest update times.

**Intent:** Records per-frame update-phase timing data for each system to power the diagnostics overlay.

**Use-case:** Queried by the diagnostics system to display which systems are consuming the most update time; not typically used directly in game code.

### ⭐ Constructors
```csharp
public UpdateTimeTracker()
```

### ⭐ Properties
#### Length
```csharp
public int Length { get; }
```
Number of recorded samples currently stored in `Sample`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Sample
```csharp
public readonly Single[] Sample;
```
Ring buffer of the most recent update delta times in milliseconds.

**Returns** \
[float[]](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### Update(double)
```csharp
public void Update(double dt)
```
Appends `dt` (in seconds, converted to ms) to the ring buffer; only active in DEBUG builds.

**Parameters** \
`dt` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \



⚡
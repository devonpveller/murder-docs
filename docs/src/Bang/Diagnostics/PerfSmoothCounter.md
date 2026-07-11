# PerfSmoothCounter

**Namespace:** Bang.Diagnostics \
**Assembly:** Bang.dll

```csharp
public class PerfSmoothCounter
```

Class used to smooth the counter of performance ticks.

### ⭐ Constructors
```csharp
public PerfSmoothCounter(int size = 500)
```

Creates a new [PerfSmoothCounter](../../Bang/Diagnostics/PerfSmoothCounter.html).

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

### ⭐ Properties
#### AverageEntities
```csharp
public int AverageEntities { get; }
```

Average of entities over the sample size.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### AverageTime
```csharp
public int AverageTime { get; }
```

Average of counter time value over the sample size.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### CurrentEntities
```csharp
public int CurrentEntities { get; }
```

The most recent entity count.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### CurrentIndex
```csharp
public int CurrentIndex { get; }
```

The index of the most recently written sample within the internal ring buffers. This wraps back to zero once it reaches the sample size, so the counter keeps overwriting the oldest entries.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### CurrentTime
```csharp
public double CurrentTime { get; }
```

The most recent time value.

**Returns** \
[double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \
#### MaximumTime
```csharp
public double MaximumTime { get; }
```

Maximum value over the sample size.

**Returns** \
[double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \
#### PAUSED
```csharp
public static bool PAUSED;
```

When set to true, [PerfSmoothCounter.Clear](../../Bang/Diagnostics/PerfSmoothCounter.html#clear) and [PerfSmoothCounter.Update](../../Bang/Diagnostics/PerfSmoothCounter.html#update) become no-ops, freezing the counter at its current values. Useful for pausing performance tracking, e.g. while a debug overlay is being inspected, without losing the last collected samples.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
### ⭐ Methods
#### Clear()
```csharp
public void Clear()
```

Clear the counter track.

#### Update(double, int)
```csharp
public void Update(double ms, int totalEntities)
```

Update the smooth counter for the FPS report.

**Parameters** \
`ms` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \
\
`totalEntities` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\



⚡
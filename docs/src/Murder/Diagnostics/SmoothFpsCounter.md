# SmoothFpsCounter

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class SmoothFpsCounter
```

This will smooth the average FPS of the game.

**Intent:** Computes a rolling-average frames-per-second value to reduce per-frame noise.

**Use-case:** Instantiate with a window size and call the update method each frame; read `Value` for the smoothed FPS to display in a HUD or diagnostics overlay.

### ⭐ Constructors
```csharp
public SmoothFpsCounter(int size)
```
Creates a new counter using a rolling window of `size` samples for averaging.

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Value
```csharp
public double Value { get; }
```

Latest FPS value.

**Returns** \
[double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \
### ⭐ Methods
#### Update(double)
```csharp
public void Update(double dt)
```
Advances the rolling average by one frame with the given delta time in seconds.

**Parameters** \
`dt` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \



⚡
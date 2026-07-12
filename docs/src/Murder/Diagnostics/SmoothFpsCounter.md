# SmoothFpsCounter

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class SmoothFpsCounter
```

This will smooth the average FPS of the game.

**Intent:** Raw instantaneous frame times are noisy — a single hitch or a single unusually fast frame would make a naive `1 / dt` FPS readout jump around distractingly. `SmoothFpsCounter` keeps a fixed-size rolling window of the last N frame delta-times and divides the window size by their sum, giving an FPS value that changes smoothly and is representative of recent performance rather than any one frame.

**Use-case:** Instantiate once with a window size (e.g. `new SmoothFpsCounter(10)` for a 10-frame moving average), call `Update(dt)` once per frame with that frame's delta time in seconds, and read `Value` whenever a smoothed FPS number is needed — typically for an on-screen FPS counter or diagnostics overlay.

### ⭐ Constructors

```csharp
public SmoothFpsCounter(int size)
```

Creates a counter that averages FPS over a rolling window of `size` frames. A larger window produces a smoother but slower-to-react value; a smaller window tracks instantaneous FPS more closely at the cost of more jitter.

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Value

```csharp
public double Value { get; }
```

Latest smoothed FPS value: the window size divided by the sum of delta times currently in the rolling window, rounded to the nearest whole number.

**Returns** \
[double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \

### ⭐ Methods

#### Update(double)

```csharp
public void Update(double dt)
```

Advances the rolling average by one frame using the given delta time (in seconds). Replaces the oldest sample in the window with `dt`, keeping a running sum so `Value` can be computed in O(1) without re-summing the whole buffer each call. Call this once per frame, typically from the engine's update loop.

**Parameters** \
`dt` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \

⚡

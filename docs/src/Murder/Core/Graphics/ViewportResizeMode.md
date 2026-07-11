# ViewportResizeMode

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum ViewportResizeMode : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

Specifies the strategy used when scaling the game viewport to fit the window.

**Intent:** Controls the trade-off between aspect-ratio preservation, pixel scaling accuracy, and letterboxing/cropping when the window is resized.

**Use-case:** Set in `ViewportResizeStyle.ResizeMode` and pass the style to `RenderContext.RefreshWindow()` to configure how the game image fills the screen on startup or window resize.

### ⭐ Properties
#### AbsoluteScale
```csharp
public static const ViewportResizeMode AbsoluteScale;
```

Scales the game buffer by an exact multiplier specified in `ViewportResizeStyle.AbsoluteScale`, ignoring the window dimensions.

**Returns** \
[ViewportResizeMode](../../../Murder/Core/Graphics/ViewportResizeMode.html) \
#### AdaptiveLetterbox
```csharp
public static const ViewportResizeMode AdaptiveLetterbox;
```

Like `KeepRatio` but with configurable positive and negative aspect-ratio allowance bands that reduce or eliminate letterbox bars by slightly adjusting the visible game area.

**Returns** \
[ViewportResizeMode](../../../Murder/Core/Graphics/ViewportResizeMode.html) \
#### Crop
```csharp
public static const ViewportResizeMode Crop;
```

Scales the game buffer to fill the entire window and crops any edges that extend beyond the window boundary.

**Returns** \
[ViewportResizeMode](../../../Murder/Core/Graphics/ViewportResizeMode.html) \
#### KeepRatio
```csharp
public static const ViewportResizeMode KeepRatio;
```

Scales the game buffer uniformly to fit the window while preserving the original aspect ratio, adding letterbox or pillarbox bars as needed.

**Returns** \
[ViewportResizeMode](../../../Murder/Core/Graphics/ViewportResizeMode.html) \
#### None
```csharp
public static const ViewportResizeMode None;
```

No scaling is applied; the game buffer is rendered at its native resolution regardless of window size.

**Returns** \
[ViewportResizeMode](../../../Murder/Core/Graphics/ViewportResizeMode.html) \
#### Stretch
```csharp
public static const ViewportResizeMode Stretch;
```

Stretches the game buffer to fill the entire window, ignoring aspect ratio.

**Returns** \
[ViewportResizeMode](../../../Murder/Core/Graphics/ViewportResizeMode.html) \


⚡
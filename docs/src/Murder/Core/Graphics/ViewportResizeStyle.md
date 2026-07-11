# ViewportResizeStyle

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct ViewportResizeStyle
```

Composite settings that fully describe how the game viewport should be scaled to fit the window.

**Intent:** Bundles a `ViewportResizeMode` with tolerance parameters (snap-to-integer, aspect-ratio allowance, rounding mode, and optional fixed scale) into a single value.

**Use-case:** Construct a `ViewportResizeStyle` with the desired mode and tolerances and pass it to `RenderContext.RefreshWindow()` at startup or on window resize.

### ⭐ Constructors
```csharp
public ViewportResizeStyle()
```

Creates a default style with `ViewportResizeMode.None` and no tolerances.

```csharp
public ViewportResizeStyle(ViewportResizeMode resizeMode, float snapToInteger, RoundingMode roundingMode, float positiveApectRatioAllowance, float negativeApectRatioAllowance)
```

Creates a fully specified style with an explicit resize mode, snap threshold, rounding mode, and aspect-ratio tolerance bands.

**Parameters** \
`resizeMode` [ViewportResizeMode](../../../Murder/Core/Graphics/ViewportResizeMode.html) \
`snapToInteger` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`roundingMode` [RoundingMode](../../../Murder/Core/RoundingMode.html) \
`positiveApectRatioAllowance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`negativeApectRatioAllowance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public ViewportResizeStyle(ViewportResizeMode resizeMode)
```

Creates a style with the given resize mode and default tolerance values.

**Parameters** \
`resizeMode` [ViewportResizeMode](../../../Murder/Core/Graphics/ViewportResizeMode.html) \

### ⭐ Properties
#### AbsoluteScale
```csharp
public readonly T? AbsoluteScale;
```

When `ResizeMode` is `AbsoluteScale`, the explicit scale factor applied to the game buffer; null otherwise.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### NegativeApectRatioAllowance
```csharp
public readonly float NegativeApectRatioAllowance;
```

Maximum aspect-ratio deviation below the target before letterboxing is applied; allows the image to be slightly taller than the window without adding bars.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### PositiveApectRatioAllowance
```csharp
public readonly float PositiveApectRatioAllowance;
```

Maximum aspect-ratio deviation above the target before letterboxing is applied; allows the image to be slightly wider than the window without adding bars.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### ResizeMode
```csharp
public readonly ViewportResizeMode ResizeMode;
```

The `ViewportResizeMode` strategy applied when the window is resized.

**Returns** \
[ViewportResizeMode](../../../Murder/Core/Graphics/ViewportResizeMode.html) \
#### RoundingMode
```csharp
public readonly RoundingMode RoundingMode;
```

Determines whether the computed scale factor is rounded to the nearest integer, floored, or ceiled to maintain pixel-perfect output.

**Returns** \
[RoundingMode](../../../Murder/Core/RoundingMode.html) \
#### SnapToInteger
```csharp
public readonly float SnapToInteger;
```

Threshold within which the scale factor is snapped to the nearest integer multiple, preserving pixel-perfect rendering without visible blurring.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡
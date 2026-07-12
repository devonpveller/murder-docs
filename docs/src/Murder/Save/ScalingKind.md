# ScalingKind

**Namespace:** Murder.Save \
**Assembly:** Murder.dll

```csharp
public sealed enum ScalingKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

The window/render scaling strategy applied by `GamePreferences.SetScalingKind`. Controls how the game window is resized (or clamped) relative to the base game resolution (`Game.DefaultWidth`/`Game.DefaultHeight`).

**Intent:** Lets a game offer a scaling preference to players — either a free-form minimum-size mode or a pixel-perfect integer multiple of the base resolution — without every game having to reimplement window-resizing math.

**Use-case:** Read from `GamePreferences.Scaling` to know the player's current preference, and call `GamePreferences.SetScalingKind` (typically from a settings/options screen) to apply a new one; the method both updates the property and resizes the game window accordingly.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Auto

```csharp
public static const ScalingKind Auto;
```

Enforces a minimum window size of twice the base resolution, otherwise leaving the window free to resize. This is the default value of `GamePreferences.Scaling`.

**Returns** \
[ScalingKind](../../Murder/Save/ScalingKind.html) \

#### Large

```csharp
public static const ScalingKind Large;
```

Enforces a minimum window size of 1280x720, otherwise leaving the window free to resize.

**Returns** \
[ScalingKind](../../Murder/Save/ScalingKind.html) \

#### OneX

```csharp
public static const ScalingKind OneX;
```

Pixel-perfect 1x scale: when not fullscreen, the window is resized to exactly match the base resolution.

**Returns** \
[ScalingKind](../../Murder/Save/ScalingKind.html) \

#### Snap

```csharp
public static const ScalingKind Snap;
```

Reserved for a "snap to nearest integer scale" mode; not currently handled by `GamePreferences.SetScalingKind`'s window-resize logic (falls through to a no-op).

**Returns** \
[ScalingKind](../../Murder/Save/ScalingKind.html) \

#### ThreeX

```csharp
public static const ScalingKind ThreeX;
```

Pixel-perfect 3x scale: when not fullscreen, the window is resized to exactly three times the base resolution.

**Returns** \
[ScalingKind](../../Murder/Save/ScalingKind.html) \

#### TwoX

```csharp
public static const ScalingKind TwoX;
```

Pixel-perfect 2x scale: when not fullscreen, the window is resized to exactly twice the base resolution.

**Returns** \
[ScalingKind](../../Murder/Save/ScalingKind.html) \

⚡

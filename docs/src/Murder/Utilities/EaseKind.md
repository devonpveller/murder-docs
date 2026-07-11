# EaseKind

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed enum EaseKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies an easing technique.

**Intent:** Enumerates all supported easing curves so that tweens and animations can specify their interpolation style declaratively.

**Use-case:** Set a `TweenComponent.EaseKind` or `MoveToPerfectComponent.EaseKind` to control the shape of a position or property animation.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### BackIn
```csharp
public static const EaseKind BackIn;
```

Overshoots slightly before the target on entry (cubic back easing, in).

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### BackInOut
```csharp
public static const EaseKind BackInOut;
```

Overshoots on both entry and exit.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### BackOut
```csharp
public static const EaseKind BackOut;
```

Overshoots past the target and snaps back on exit.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### BackOutSm
```csharp
public static const EaseKind BackOutSm;
```

A smaller overshoot variant of `BackOut`.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### BounceIn
```csharp
public static const EaseKind BounceIn;
```

Simulates a bouncing entry — the value bounces before reaching the start.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### BounceInOut
```csharp
public static const EaseKind BounceInOut;
```

Bounces on both entry and exit.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### BounceOut
```csharp
public static const EaseKind BounceOut;
```

Simulates a bouncing stop — the value bounces after reaching the target.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### CircIn
```csharp
public static const EaseKind CircIn;
```

Circular easing — accelerates from rest following a circular curve.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### CircInOut
```csharp
public static const EaseKind CircInOut;
```

Circular easing in and out.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### CircOut
```csharp
public static const EaseKind CircOut;
```

Circular easing — decelerates to rest following a circular curve.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### CubeIn
```csharp
public static const EaseKind CubeIn;
```

Cubic easing (t³) — slow start, accelerates toward the target.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### CubeInOut
```csharp
public static const EaseKind CubeInOut;
```

Cubic easing in and out — slow at both ends.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### CubeOut
```csharp
public static const EaseKind CubeOut;
```

Cubic easing (1 - (1-t)³) — fast start, decelerates to the target.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### ElasticIn
```csharp
public static const EaseKind ElasticIn;
```

Elastic easing — oscillates at the start before moving toward the target.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### ElasticInOut
```csharp
public static const EaseKind ElasticInOut;
```

Elastic easing oscillating at both ends.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### ElasticOut
```csharp
public static const EaseKind ElasticOut;
```

Elastic easing — oscillates past the target before settling.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### ExpoIn
```csharp
public static const EaseKind ExpoIn;
```

Exponential easing — very slow start with a sharp accelerating curve.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### ExpoInOut
```csharp
public static const EaseKind ExpoInOut;
```

Exponential easing in and out.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### ExpoOut
```csharp
public static const EaseKind ExpoOut;
```

Exponential easing — sharp start that decelerates to the target.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### Linear
```csharp
public static const EaseKind Linear;
```

Linear interpolation — constant rate of change with no easing.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### QuadIn
```csharp
public static const EaseKind QuadIn;
```

Quadratic easing (t²) — slow start.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### QuadInOut
```csharp
public static const EaseKind QuadInOut;
```

Quadratic easing in and out — slow at both ends.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### QuadOut
```csharp
public static const EaseKind QuadOut;
```

Quadratic easing (1 - (1-t)²) — fast start, decelerates.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### QuartIn
```csharp
public static const EaseKind QuartIn;
```

Quartic easing (t⁴) — very slow start.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### QuartInOut
```csharp
public static const EaseKind QuartInOut;
```

Quartic easing in and out.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### QuartOut
```csharp
public static const EaseKind QuartOut;
```

Quartic easing — fast start, decelerates sharply.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### QuintIn
```csharp
public static const EaseKind QuintIn;
```

Quintic easing (t⁵) — extremely slow start.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### QuintInOut
```csharp
public static const EaseKind QuintInOut;
```

Quintic easing in and out.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### QuintOut
```csharp
public static const EaseKind QuintOut;
```

Quintic easing — extremely fast start, decelerates.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### SineIn
```csharp
public static const EaseKind SineIn;
```

Sinusoidal easing — smooth acceleration following a sine curve.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### SineInOut
```csharp
public static const EaseKind SineInOut;
```

Sinusoidal easing in and out.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### SineOut
```csharp
public static const EaseKind SineOut;
```

Sinusoidal easing — smooth deceleration following a sine curve.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### ToAndFro
```csharp
public static const EaseKind ToAndFro;
```

Eases to the target value and then back, creating a ping-pong effect.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### ZeroToOne
```csharp
public static const EaseKind ZeroToOne;
```

A simple 0-to-1 ramp with no easing.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \


⚡
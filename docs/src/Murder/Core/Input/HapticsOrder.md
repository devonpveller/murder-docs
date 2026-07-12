# HapticsOrder

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct HapticsOrder
```

A single timed gamepad rumble effect: a vibration-intensity curve (start/middle/end) and a left/right motor balance curve, each sampled over the effect's time window.

**Intent:** Describe one rumble effect declaratively — an intensity ramp and a directional balance ramp over a start/end time — so `HapticsManager` can sample and mix many concurrent effects without each caller managing per-frame vibration math itself.

**Use-case:** Building one directly is uncommon — prefer the `HapticsServices` helper methods (`Vibrate`, `VibrateInversePulse`, `HitLeft`/`HitRight`), which construct pre-tuned orders for a rumble pulse or a directional impact. When you do need a custom effect, construct one with an object initializer and pass it to `HapticsManager.Add`.

### ⭐ Constructors

```csharp
public HapticsOrder()
```

Creates a haptic order with all curves defaulted to zero vibration and centered (0.5) balance; set the desired fields via object initializer before passing to `HapticsManager.Add`.

### ⭐ Properties

#### BalanceEnd

```csharp
public readonly float BalanceEnd { get; init; }
```

Left/right motor balance (0 = fully left motor, 1 = fully right motor, 0.5 = even) at `EndTime`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### BalanceMiddle

```csharp
public readonly float BalanceMiddle { get; init; }
```

Left/right motor balance at the midpoint between `StartTime` and `EndTime`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### BalanceStart

```csharp
public readonly float BalanceStart { get; init; }
```

Left/right motor balance at `StartTime`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### EndTime

```csharp
public readonly float EndTime { get; init; }
```

The `Game.NowUnscaled` timestamp this effect ends at and is removed from `HapticsManager`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### EndVibration

```csharp
public readonly float EndVibration { get; init; }
```

Vibration intensity (0-1) at `EndTime`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### MiddleVibration

```csharp
public readonly float MiddleVibration { get; init; }
```

Vibration intensity (0-1) at the midpoint between `StartTime` and `EndTime`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Player

```csharp
public readonly PlayerIndex Player { get; init; }
```

Which controller slot this effect targets.

**Returns** \
[PlayerIndex](https://docs.monogame.net/api/Microsoft.Xna.Framework.PlayerIndex.html) \

#### StartTime

```csharp
public readonly float StartTime { get; init; }
```

The `Game.NowUnscaled` timestamp this effect begins at.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### StartVibration

```csharp
public readonly float StartVibration { get; init; }
```

Vibration intensity (0-1) at `StartTime`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

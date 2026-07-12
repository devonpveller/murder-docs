# HapticsServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class HapticsServices
```

Helpers for queuing gamepad rumble/vibration effects through `Game.Instance.Haptics`.

**Intent:** Provides named, intention-revealing shortcuts (`Vibrate`, `VibrateInversePulse`, `HitLeft`, `HitRight`, `StopVibration`) over constructing a `Core.Input.HapticsOrder` by hand, each pre-configuring the start/middle/end vibration and left/right balance envelope for a specific feel.

**Use-case:** Call `HitLeft`/`HitRight` for directional impact feedback (e.g. taking a hit from the left or right side), `Vibrate` for a flat, sustained rumble, `VibrateInversePulse` for an effect that pulses from silent to full and pans across the controller, and `StopVibration` to immediately cancel any ongoing haptics — for example when the player pauses the game or a cutscene starts.

### ⭐ Methods

#### StopVibration()

```csharp
public static void StopVibration()
```

Stops any ongoing vibration for `PlayerIndex.One`. Shorthand for `StopVibration(PlayerIndex.One)`.

#### Vibrate(float, float, float, PlayerIndex)

```csharp
public static void Vibrate(float vibration, float balance, float durationSeconds, PlayerIndex player = PlayerIndex.One)
```

Queues a flat-intensity vibration: `vibration` is used for both the start and middle envelope points (tapering to `0` at the end), held at a constant `balance` for `durationSeconds`. Use this for a simple, sustained rumble that doesn't need a directional or pulsing feel.

**Parameters** \
`vibration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`balance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`durationSeconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`player` [PlayerIndex](https://docs.monogame.net/api/Microsoft.Xna.Framework.PlayerIndex.html) \

#### VibrateInversePulse(float, float, PlayerIndex)

```csharp
public static void VibrateInversePulse(float vibration, float durationSeconds, PlayerIndex player = PlayerIndex.One)
```

Queues a vibration that starts at `vibration`, dips to `0` in the middle, and rises back to `vibration` at the end, while its stereo balance sweeps from `0` to `1`. Use this for a distinct "pulse that pans across the controller" feel, different from the flat rumble of `Vibrate`.

**Parameters** \
`vibration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`durationSeconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`player` [PlayerIndex](https://docs.monogame.net/api/Microsoft.Xna.Framework.PlayerIndex.html) \

#### HitRight(float, float, PlayerIndex)

```csharp
public static void HitRight(float vibration, float duration, PlayerIndex player = PlayerIndex.One)
```

Queues a directional "hit from the right" impact: vibration ramps from half-strength up to full and back to `0`, with the balance envelope weighted toward the right side of the controller (`1 → 0.5 → 0.65`). Use for feedback when the player is struck or bumped from their right.

**Parameters** \
`vibration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`player` [PlayerIndex](https://docs.monogame.net/api/Microsoft.Xna.Framework.PlayerIndex.html) \

#### HitLeft(float, float, PlayerIndex)

```csharp
public static void HitLeft(float vibration, float duration, PlayerIndex player = PlayerIndex.One)
```

Queues a directional "hit from the left" impact, mirroring `HitRight` but with the balance envelope weighted toward the left side (`1 → 0.5 → 0.4`). Use for feedback when the player is struck or bumped from their left.

**Parameters** \
`vibration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`player` [PlayerIndex](https://docs.monogame.net/api/Microsoft.Xna.Framework.PlayerIndex.html) \

#### StopVibration(PlayerIndex)

```csharp
public static void StopVibration(PlayerIndex player)
```

Immediately clears any ongoing vibration order for `player` via `Game.Instance.Haptics.ClearVibration`. Use when haptics need to be cut off instantly rather than left to fade out (e.g. pausing, or the player character dying).

**Parameters** \
`player` [PlayerIndex](https://docs.monogame.net/api/Microsoft.Xna.Framework.PlayerIndex.html) \

⚡

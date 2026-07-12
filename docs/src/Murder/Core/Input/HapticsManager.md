# HapticsManager

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class HapticsManager
```

Owns and mixes every active gamepad rumble/vibration request.

**Intent:** Accumulate `HapticsOrder` entries and, every frame, blend their per-controller left/right motor intensities together before pushing the combined value to FNA's gamepad vibration API — so multiple simultaneous haptic effects (e.g. a hit pulse layered over an ambient rumble) combine sensibly instead of each caller fighting over `GamePad.SetVibration` directly.

**Use-case:** Accessible via `Game.Instance.Haptics` (one instance per `Game`). Prefer the `HapticsServices` static helpers (`Vibrate`, `VibrateInversePulse`, `HitLeft`, `HitRight`) over calling `Add` directly — they construct pre-tuned `HapticsOrder` values for common cases. `Update()` and `ClearAll()` are called by the engine; game code should not need to call them directly.

### ⭐ Constructors

```csharp
public HapticsManager()
```

### ⭐ Methods

#### Add(HapticsOrder)

```csharp
public void Add(HapticsOrder order)
```

Queues a new haptic effect to be mixed in on subsequent `Update()` calls until its `HapticsOrder.EndTime` is reached.

**Parameters** \
`order` [HapticsOrder](../../../Murder/Core/Input/HapticsOrder.html) \
The haptic effect to queue. \

#### ClearAll()

```csharp
public void ClearAll()
```

Cancels every queued haptic order and immediately zeroes vibration on every connected controller. Called on scene/game shutdown to make sure rumble doesn't keep running after gameplay stops.

#### Update()

```csharp
public void Update()
```

Advances every active `HapticsOrder` by one frame: computes each order's current vibration/balance from its time curve, mixes them per controller (taking the strongest value per motor), removes orders that have finished, and pushes the final left/right motor speeds — scaled by the player's haptics volume preference — to every connected gamepad. Called once per frame by the engine.

⚡

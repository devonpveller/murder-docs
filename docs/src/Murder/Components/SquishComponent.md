# SquishComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SquishComponent : IComponent
```

Drives a short squash-and-stretch animation on an entity's scale, typically used as a hit-reaction or bounce effect.

**Intent:** Play a timed scale squish/stretch animation without needing a dedicated animation asset or hand-written tween code.

**Use-case:** Add to an entity when it takes a hit or lands a jump. `SquishSystem` (filtering on `PositionComponent` + `SquishComponent`, running in `BeforeDraw`) computes a normalized time from `Start`/`Duration` (using `Game.Now` or `Game.NowUnscaled` depending on `ScaledTime`), evaluates the eased rate via `Ease.Evaluate`, and calls `Entity.SetScale(Vector2Helper.Squish(easedRate * Amount))` every frame. If `EaseIn` is set, the first half of the animation (`time <= 0.5`) uses `EaseIn` and the second half uses `EaseOut` (defaulting to `EaseKind.Linear` if unset) for a squish-then-recover motion; if only `EaseOut` is set, the whole animation eases out from full squish back to rest. Once `time >= 1`, the system removes both `SquishComponent` and the entity's scale override. Marked `[RuntimeOnly]` and `[DoNotPersistOnSave]` since it is a transient, self-removing effect.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SquishComponent(EaseKind easeOut, float start, float duration, float amount)
```

Creates a squish that only eases out (recovers) from full `amount` back to rest — no separate squish-in phase.

**Parameters** \
`easeOut` [EaseKind](../../Murder/Utilities/EaseKind.html) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public SquishComponent(EaseKind easeIn, EaseKind easeOut, float start, float duration, float amount)
```

Creates a squish with distinct ease curves for the squish-in (first half) and recovery (second half) phases.

**Parameters** \
`easeIn` [EaseKind](../../Murder/Utilities/EaseKind.html) \
`easeOut` [EaseKind](../../Murder/Utilities/EaseKind.html) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Amount

```csharp
public readonly float Amount;
```

Peak squish magnitude fed into `Vector2Helper.Squish(amount)`, which produces a scale of `(1 + amount, 1 - amount)`. Positive values widen the entity horizontally and flatten it vertically (a squash); negative values do the opposite (a vertical stretch).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Duration

```csharp
public readonly float Duration;
```

Total duration of the squish animation in seconds, measured from `Start`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### EaseIn

```csharp
public readonly EaseKind? EaseIn;
```

Optional ease curve for the first half (squish-in) of the animation. When `null`, the animation has no separate squish-in phase and uses only `EaseOut` for the whole duration.

**Returns** \
[EaseKind?](../../Murder/Utilities/EaseKind.html) \

#### EaseOut

```csharp
public readonly EaseKind? EaseOut;
```

Ease curve applied to the recovery (second) half of the animation, or to the full animation if `EaseIn` is `null`. Falls back to `EaseKind.Linear` if left unset while `EaseIn` is set.

**Returns** \
[EaseKind?](../../Murder/Utilities/EaseKind.html) \

#### ScaledTime

```csharp
public readonly bool ScaledTime { get; init; }
```

When true, the animation advances using game-scaled time; when false, it uses unscaled real time.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Start

```csharp
public readonly float Start;
```

Game time (in seconds) at which the squish animation begins.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

# FadeTransitionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeTransitionComponent : IComponent
```

Drives a linear-time, eased alpha transition on an entity, applied by writing to its [AlphaComponent](../../Murder/Components/AlphaComponent.html) every frame.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Animates an entity's alpha from `StartAlpha` to `TargetAlpha` over `Duration` seconds using a cube-out ease, driven entirely by `FadeTransitionSystem` — you only need to attach the component and the system takes care of interpolating and, optionally, cleaning up afterward. Because it writes `AlphaComponent`, it affects any renderer that already respects that component's alpha (most notably sprites), not sprites exclusively.

**Use-case:** Attach to any entity that should fade in or out over time, such as a dying enemy or a highlighted item fading away. `StartTime` is `[JsonIgnore]`d, so an instance restored from a saved/serialized entity comes back with `StartTime` at its default (`0`); `FadeTransitionSystem.OnAdded` detects that (`StartTime == 0`) and re-issues the component with `StartTime` set to `Game.Now` and `StartAlpha` taken from the entity's current `AlphaComponent` (or `1` if it has none), so a restored fade always resumes correctly instead of jumping. Set `DestroyEntityOnEnd` to `true` for one-shot effects that should destroy themselves once the fade finishes; otherwise the component is simply removed, leaving the entity at `TargetAlpha`.

### ⭐ Constructors

```csharp
public FadeTransitionComponent(float duration, float startAlpha, float targetAlpha, bool destroyOnEnd)
```

**Parameters** \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startAlpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`targetAlpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`destroyOnEnd` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public FadeTransitionComponent(float duration, float startAlpha, float targetAlpha)
```

**Parameters** \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startAlpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`targetAlpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### DestroyEntityOnEnd

```csharp
public readonly bool DestroyEntityOnEnd;
```

When `true`, the entity is destroyed once the fade completes.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Duration

```csharp
public readonly float Duration;
```

Fade duration in seconds.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### StartAlpha

```csharp
public readonly float StartAlpha;
```

The initial alpha value at the beginning of the transition (range `0`–`1`).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### StartTime

```csharp
public readonly float StartTime;
```

The game time (in seconds) when the transition started; used internally to compute interpolation progress.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TargetAlpha

```csharp
public readonly float TargetAlpha;
```

The final alpha value at the end of the transition (range `0`–`1`).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

# FadeTransitionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeTransitionComponent : IComponent
```

For now, this will only fade out sprite components.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Animates an entity's sprite alpha from `StartAlpha` to `TargetAlpha` over `Duration` seconds.

**Use-case:** Attach to any sprite entity that should fade in or fade out; set `DestroyEntityOnEnd` to `true` for one-shot effects that should clean themselves up.

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
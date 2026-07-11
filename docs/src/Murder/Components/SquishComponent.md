# SquishComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SquishComponent : IComponent
```

Drives a short squash-and-stretch animation on an entity's scale, typically used as a hit-reaction or bounce effect.

**Intent:** Play a timed scale squish animation without needing a dedicated animation asset.

**Use-case:** Add to an entity when it takes a hit or lands a jump; the system interpolates the scale using the specified ease curves over `Duration` seconds, then removes the component.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public SquishComponent(EaseKind easeIn, EaseKind easeOut, float start, float duration, float amount)
```

**Parameters** \
`easeIn` [EaseKind](../../Murder/Utilities/EaseKind.html) \
`easeOut` [EaseKind](../../Murder/Utilities/EaseKind.html) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public SquishComponent(EaseKind easeOut, float start, float duration, float amount)
```

**Parameters** \
`easeOut` [EaseKind](../../Murder/Utilities/EaseKind.html) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Amount
```csharp
public readonly float Amount;
```

Peak squish/stretch magnitude; positive values stretch, negative values compress.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Duration
```csharp
public readonly float Duration;
```

Total duration of the squish animation in seconds.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### EaseIn
```csharp
public readonly T? EaseIn;
```

Optional ease curve for the first half of the squish animation. Null uses a single ease-out curve for the whole animation.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### EaseOut
```csharp
public readonly T? EaseOut;
```

Ease curve applied to the recovery (or the full animation if `EaseIn` is null).

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### ScaledTime
```csharp
public bool ScaledTime { get; public set; }
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
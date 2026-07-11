# TweenComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TweenComponent : IComponent
```

Drives a tween animation that interpolates an entity's position and/or scale over a time range using a configurable ease function.

**Intent:** Describe a time-based lerp animation on an entity's transform properties.

**Use-case:** Add to an entity to animate it moving or scaling between two values; remove the component when the tween is no longer needed or when `Time.Max` is reached.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public TweenComponent()
```

```csharp
public TweenComponent(float timeStart, float timeEnd)
```

**Parameters** \
`timeStart` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`timeEnd` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Ease
```csharp
public EaseKind Ease { get; public set; }
```

Ease function applied to the interpolation across the time range.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### Position
```csharp
public T? Position { get; public set; }
```

Optional position tween; when set the entity's position is interpolated from `From` to `To` over `Time`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Scale
```csharp
public T? Scale { get; public set; }
```

Optional scale tween; when set the entity's scale is interpolated from `From` to `To` over `Time`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Time
```csharp
public FloatRange Time { get; public set; }
```

Game-time range (start, end) over which the tween progresses.

**Returns** \
[FloatRange](../../Murder/Core/FloatRange.html) \


⚡
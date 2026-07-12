# TweenComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TweenComponent : IComponent
```

Drives a one-shot tween that interpolates an entity's position and/or scale over an absolute time range using a configurable ease function.

**Intent:** Describe a time-based lerp animation on an entity's transform properties without hand-writing per-frame interpolation code.

**Use-case:** Add to an entity to animate it moving or scaling between two values. `TweenSystem` computes progress each frame as `ClampTime(Game.Now - Time.Start, Time.End - Time.Start, Ease)`, applies it to whichever of `Position`/`Scale` is set, and automatically removes the component once progress reaches `1` — callers do not need to remove it themselves. Note that `Time`'s start/end are absolute timestamps compared against `Game.Now` (typically `Game.Now` and `Game.Now + duration`), not a relative duration.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public TweenComponent()
```

Creates a tween with a default (zero-length) time range; set `Time` via an object initializer before use.

```csharp
public TweenComponent(float timeStart, float timeEnd)
```

Creates a tween spanning the absolute time range `timeStart` to `timeEnd`. Typically called with `Game.Now` and `Game.Now + duration`.

**Parameters** \
`timeStart` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`timeEnd` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Ease

```csharp
public EaseKind Ease { get; public set; }
```

Ease function applied when mapping elapsed time within `Time` to progress.

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \

#### Position

```csharp
public T? Position { get; public set; }
```

Optional position tween; when set, the entity's position is interpolated across `Time` from [Vector2FromTo](../../Murder/Components/Vector2FromTo.html).From to `.To`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Scale

```csharp
public T? Scale { get; public set; }
```

Optional scale tween; when set, the entity's scale is interpolated across `Time` from [Vector2FromTo](../../Murder/Components/Vector2FromTo.html).From to `.To`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Time

```csharp
public FloatRange Time { get; public set; }
```

Absolute `Game.Now` timestamp range (start, end) over which the tween progresses.

**Returns** \
[FloatRange](../../Murder/Core/FloatRange.html) \

⚡

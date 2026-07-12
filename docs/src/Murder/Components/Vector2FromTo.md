# Vector2FromTo

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
sealed struct Vector2FromTo
```

Represents a pair of `Vector2` values (a start point and an end point) used by [TweenComponent](../../Murder/Components/TweenComponent.html) to define a positional or scale animation range.

**Intent:** Bundle the start and end vectors of a tween channel into a single value that `TweenComponent` can hold as an optional `Position` or `Scale` payload.

**Use-case:** Assign to `TweenComponent.Position` or `TweenComponent.Scale` to specify the from/to range for that tween channel; `TweenSystem` interpolates between `From` and `To` each frame based on the tween's progress.

### ⭐ Constructors

```csharp
public Vector2FromTo(Vector2 from, Vector2 to)
```

Creates a tween range from `from` to `to`.

**Parameters** \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`to` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### From

```csharp
public Vector2 From { get; public set; }
```

Value at the start of the tween (progress `0`).

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### To

```csharp
public Vector2 To { get; public set; }
```

Value at the end of the tween (progress `1`).

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

# Vector2FromTo

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
sealed struct Vector2FromTo
```

Represents a pair of `Vector2` values (a start point and an end point) used by [TweenComponent](../../Murder/Components/TweenComponent.html) to define a positional or scale animation range.

**Intent:** Bundle the start and end vectors of a tween channel into a single value.

**Use-case:** Assign to `TweenComponent.Position` or `TweenComponent.Scale` to specify the from/to range for that tween channel.

### ⭐ Constructors
```csharp
public Vector2FromTo(Vector2 from, Vector2 to)
```

**Parameters** \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`to` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties
#### From
```csharp
public Vector2 From { get; public set; }
```

Start value of the tween at progress 0.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### To
```csharp
public Vector2 To { get; public set; }
```

End value of the tween at progress 1.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \


⚡
# MoveToPerfectComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct MoveToPerfectComponent : IComponent
```

This is a move to component that is not tied to any agent and
            that matches perfectly the target.

**Intent:** Move an entity to an exact world-space position over a fixed duration using a chosen easing function, independent of agent speed or physics.

**Use-case:** Add to objects that need smooth, deterministic tweened movement (e.g. a projectile arcing to a point, a UI element sliding in); the `MoveToPerfectSystem` updates position each frame and removes the component on arrival.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public MoveToPerfectComponent(Vector2& target, float duration, EaseKind ease)
```

**Parameters** \
`target` [Vector2&](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`ease` [EaseKind](../../Murder/Utilities/EaseKind.html) \

### ⭐ Properties
#### Duration
```csharp
public readonly float Duration;
```

Total duration (in seconds) for the entity to travel from start to target.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### EaseKind
```csharp
public readonly EaseKind EaseKind;
```

Easing function applied to the movement interpolation (e.g. linear, ease-in, ease-out).

**Returns** \
[EaseKind](../../Murder/Utilities/EaseKind.html) \
#### StartPosition
```csharp
public readonly T? StartPosition;
```

Optional explicit starting position; if `null`, the entity's current position at the time movement begins is used.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### StartTime
```csharp
public readonly float StartTime;
```

Absolute game time (in seconds) when the tween movement began, used to compute normalized progress each frame.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Target
```csharp
public readonly Vector2 Target;
```

World-space destination position the entity will reach at the end of the tween.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
### ⭐ Methods
#### WithStartPosition(Vector2&)
```csharp
public MoveToPerfectComponent WithStartPosition(Vector2& startPosition)
```

**Parameters** \
`startPosition` [Vector2&](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[MoveToPerfectComponent](../../Murder/Components/MoveToPerfectComponent.html) \



⚡
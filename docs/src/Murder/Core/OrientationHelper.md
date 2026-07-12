# OrientationHelper

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public static class OrientationHelper
```

Static helper methods for deriving an `Orientation` (and how strongly it applies) from a raw movement or facing `Vector2`.

**Intent:** Turns a continuous 2D direction/velocity vector into a discrete axis classification (horizontal vs. vertical) or a continuous 0-1 weight along a chosen axis, so gameplay systems can reason about "mostly horizontal" or "mostly vertical" movement without hand-rolling the trigonometry each time.

**Use-case:** `MovementModAreaComponent`/`AgentMoverSystem` use `GetOrientationAmount` to scale how strongly an area's slide force or speed multiplier applies based on how aligned an agent's current movement is with the area's configured `Orientation`. `GetDominantOrientation` is available for picking between horizontal/vertical animation sets or blend weights based on an agent's current velocity, though no system currently calls it.

### ⭐ Methods

#### GetOrientationAmount(Vector2, Orientation)

```csharp
public static float GetOrientationAmount(Vector2 vector, Orientation orientation)
```

Returns how much of `vector`'s magnitude is attributable to `orientation`, expressed as a 0-1 fraction of the sum of the absolute X and Y components. Passing `Orientation.Both` always returns `1`. This is the method `AgentMoverSystem` calls when an agent is inside a `MovementModAreaComponent` zone: it multiplies the area's `SpeedMultiplier` influence by this value, so a slide zone oriented `Horizontal` only fully applies its multiplier when the agent is moving mostly left/right.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`orientation` [Orientation](../../Murder/Core/Orientation.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetDominantOrientation(Vector2)

```csharp
public static Orientation GetDominantOrientation(Vector2 vector)
```

Determines whether `vector` is predominantly horizontal or vertical by comparing the magnitude of its X and Y components. Ties (equal magnitude) resolve to `Orientation.Vertical`. Never returns `Orientation.Both`.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \

⚡

# VerticalPositionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct VerticalPositionComponent : IComponent
```

Tracks the vertical (Z-axis) position and velocity of an entity in a top-down 2.5D game. The entity can be above the ground and optionally subject to gravity.

**Intent:** Add a height dimension to otherwise-2D entities, for jump arcs, thrown/knocked-back objects and bouncing projectiles, without a full 3D transform.

**Use-case:** Attach to characters or objects that can jump or be thrown. Every fixed tick, `VerticalPhysicsSystem` calls `UpdatePosition` on any entity carrying this component to advance `Z`/`ZVelocity` under gravity, bounce it off the ground once `Z` reaches `0`, and remove the component entirely once it comes to rest. Set `HasGravity` to `false` for floating objects that should stay at a fixed height. This component only tracks the height value itself — it does not affect the entity's X/Y position or collision; render systems commonly read `Z` to offset the sprite's draw position and simulate a jump.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public VerticalPositionComponent()
```

Creates a component at ground level (`Z = 0`), at rest, with gravity enabled.

```csharp
public VerticalPositionComponent(float z, float zVelocity, bool hasGravity)
```

Creates a component with an explicit height, vertical velocity, and gravity setting.

**Parameters** \
`z` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`zVelocity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`hasGravity` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### GRAVITY

```csharp
public static const float GRAVITY;
```

Named base gravity constant (`0.1`). Not referenced by `UpdatePosition`, which instead hard-codes its own acceleration figure combined with an externally supplied multiplier; kept as a documented reference value for callers that want one.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### HasGravity

```csharp
public readonly bool HasGravity;
```

When `true` (the default), `UpdatePosition` accelerates `ZVelocity` towards the ground each tick. When `false`, `UpdatePosition` is a no-op and the entity stays at a fixed height, floating in place.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Z

```csharp
public readonly float Z;
```

Current vertical height above the ground in pixels (`0` = on the ground).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ZVelocity

```csharp
public readonly float ZVelocity;
```

Current vertical velocity in pixels per second. Positive values move the entity down towards the ground (falling); negative values move it up, away from the ground (e.g. right after a jump launch or a bounce).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### UpdatePosition(float, float, float)

```csharp
public VerticalPositionComponent UpdatePosition(float deltaTime, float bounciness, float multiplier)
```

Advances the vertical physics simulation by one fixed tick: applies gravity acceleration (scaled by `multiplier`) to `ZVelocity`, clamps fall speed to a maximum of `200`, moves `Z`, and — if the entity reaches the ground — bounces it back up by `bounciness`, zeroing out the velocity entirely once the bounce becomes negligible. Returns the component unchanged when `HasGravity` is `false`.

**Parameters** \
`deltaTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bounciness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`multiplier` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[VerticalPositionComponent](../../Murder/Components/VerticalPositionComponent.html) \

⚡

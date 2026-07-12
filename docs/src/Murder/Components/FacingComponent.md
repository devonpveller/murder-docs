# FacingComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FacingComponent : IComponent
```

Stores the direction and angle an entity is currently facing.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a single source of truth for an entity's facing direction so animation, physics, and AI systems all read the same value. It carries `[KeepOnReplace]`, so when an entity's components are replaced (e.g. re-instantiating from a prefab), the entity keeps its current facing instead of resetting to the prefab's default.

**Use-case:** Attach to any entity that has directional sprite animations or directional behavior. `AgentSpriteSystem` reads `Direction` (rounded to 4/8-way or restricted to horizontal/vertical, depending on the sprite's facing configuration) to pick the animation suffix and flip state via `SpriteFacingComponent`/`AgentSpriteComponent`. Prefer constructing from a `Direction` when snapping to a discrete facing (e.g. gamepad input); construct from an angle when the source is continuous (e.g. aiming at a mouse position or another entity).

### ⭐ Constructors

```csharp
public FacingComponent(Direction direction)
```

Creates a FacingComponent using a Direction as a base.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \
\

```csharp
public FacingComponent(float angle)
```

Creates a FacingComponent from an angle in radians, deriving the nearest cardinal or diagonal direction automatically.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Angle

```csharp
public readonly float Angle;
```

The angle the agent is facing, in radians

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Direction

```csharp
public Direction Direction { get; }
```

The [FacingComponent.Direction](../../Murder/Components/FacingComponent.html#direction) that this entity is facing

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

⚡

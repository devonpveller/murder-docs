# MovementModAreaComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct MovementModAreaComponent : IComponent
```

Defines a collision area that modifies agent movement by applying a speed multiplier and/or a directional slide force to agents inside it.

**Intent:** Create environmental zones (e.g. mud, ice, conveyor belts, water currents) that alter how fast or in what direction agents move while inside.

**Use-case:** Add to a trigger entity that represents the zone; configure `SpeedMultiplier` (0 = stop, >1 = accelerate) and `Slide` with an `Orientation` to push agents in a set direction.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public MovementModAreaComponent()
```

Default constructor used by the editor/serializer; leaves `GroundedOnly` at `true`, `Slide`/`SpeedMultiplier` at `0`, `Orientation` at its default, and `AffectOnly` empty (affects every agent).

```csharp
public MovementModAreaComponent(bool groundedOnly, float speedMultiplier, float slide, Orientation orientation, Tags affectOnly)
```

Creates a fully configured area with an explicit grounded-only flag, speed multiplier, slide strength, slide orientation, and tag filter, for building the zone in code rather than through the editor inspector.

**Parameters** \
`groundedOnly` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`speedMultiplier` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`slide` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`orientation` [Orientation](../../Murder/Core/Orientation.html) \
`affectOnly` [Tags](../../Murder/Core/Tags.html) \

### ⭐ Properties

#### AffectOnly

```csharp
public readonly Tags AffectOnly;
```

Tag filter restricting which agents are affected by this area; an empty tag set means all agents are affected.

**Returns** \
[Tags](../../Murder/Core/Tags.html) \

#### GroundedOnly

```csharp
public readonly bool GroundedOnly;
```

When `true`, the movement modifier is applied only to agents that are currently grounded.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Orientation

```csharp
public readonly Orientation Orientation;
```

Axis along which the `Slide` force is applied to agents inside this area.

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \

#### Slide

```csharp
public readonly float Slide;
```

Constant force (in units/second) applied along the `Orientation` axis to push agents through the area.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SpeedMultiplier

```csharp
public readonly float SpeedMultiplier;
```

Multiplier applied to the agent's movement speed while inside this area (0 = stop, 1 = normal speed, >1 = faster).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

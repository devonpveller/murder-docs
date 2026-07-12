# CameraFollowComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct CameraFollowComponent : IComponent
```

Component used by the camera for tracking its target position.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Marks the entity the camera should track and configures how it should approach that target — via a dead zone, instant centering, an exact pixel-perfect follow, or by simply holding its current position. `[Unique]`, so only one entity in the world can carry this component at a time; that entity is fetched with `world.GetUniqueEntityCameraFollow()`.

**Use-case:** Attach to the unique entity that owns camera-follow state (fetched via `world.GetUniqueEntityCameraFollow()`); [CameraServices](../../Murder/Services/CameraServices.html) exposes `AddSecondaryTarget`/`RemoveSecondaryTarget` helpers that replace this component to blend in a second point of interest (e.g. a boss during a fight) without losing the primary target. `Style`, `SecondaryTarget`, and `TargetPosition` are the data a game-specific camera-tracking system is expected to read each frame to decide where the camera should move; the Murder engine itself only provides this component and the `CameraServices` helpers for mutating it, not a built-in system that moves the camera from it.

### ⭐ Constructors

```csharp
public CameraFollowComponent()
```

```csharp
public CameraFollowComponent(Point targetPosition)
```

**Parameters** \
`targetPosition` [Point](../../Murder/Core/Geometry/Point.html) \

```csharp
public CameraFollowComponent(bool enabled, Entity secondaryTarget)
```

**Parameters** \
`enabled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`secondaryTarget` [Entity](../../Bang/Entities/Entity.html) \

```csharp
public CameraFollowComponent(bool enabled, CameraStyle style)
```

**Parameters** \
`enabled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`style` [CameraStyle](../../Murder/Components/CameraStyle.html) \

```csharp
public CameraFollowComponent(bool enabled)
```

**Parameters** \
`enabled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### Enabled

```csharp
public readonly bool Enabled;
```

Whether camera following is currently active for this entity.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SecondaryTarget

```csharp
public readonly Entity SecondaryTarget;
```

Optional secondary entity whose position should be blended with the primary target to produce the final camera position, set via `CameraServices.AddSecondaryTarget`. Not serialized (`[JsonIgnore]`).

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### Style

```csharp
public readonly CameraStyle Style;
```

Determines how the camera approaches its target: `DeadZone` (the default — only moves once the target leaves a dead-zone rectangle), `Center` (keeps the target exactly centered), `Perfect` (pixel-perfect tracking), or `KeepPosition` (camera stays where it is regardless of the target). Not serialized (`[JsonIgnore]`).

**Returns** \
[CameraStyle](../../Murder/Components/CameraStyle.html) \

#### Speed

```csharp
public readonly float Speed { get; public set; }
```

Interpolation speed used when moving the camera toward its target; defaults to `1`. Tagged `[HideInEditor]`, so it is not exposed in the entity inspector.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TargetPosition

```csharp
public readonly Point? TargetPosition;
```

Optional fixed world-space position the camera should move toward, set by the `CameraFollowComponent(Point)` constructor; when set, `Style` is forced to `CameraStyle.Center`. Not serialized (`[JsonIgnore]`).

**Returns** \
[Point?](../../Murder/Core/Geometry/Point.html) \

⚡

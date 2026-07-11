# CameraFollowComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct CameraFollowComponent : IComponent
```

Component used by the camera for tracking its target position.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Marks an entity as the camera's follow target and configures how the camera interpolates toward it.

**Use-case:** Attach to the player entity (or a dedicated camera target entity) so `CameraFollowSystem` knows which entity to track and with which `CameraStyle`.

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

Optional secondary entity whose position is blended with the primary target to produce the final camera position.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
#### Style
```csharp
public readonly CameraStyle Style;
```

Force to centralize the camera without a dead zone.

**Returns** \
[CameraStyle](../../Murder/Components/CameraStyle.html) \
#### TargetPosition
```csharp
public readonly T? TargetPosition;
```

Optional fixed world-space position the camera should move toward; overrides entity tracking when set.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \


⚡
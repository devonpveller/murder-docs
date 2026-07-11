# AreaInfo

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
sealed struct AreaInfo
```

Snapshot of the movement-modifying properties of a `MovementModAreaComponent` that an agent is currently inside.

**Intent:** Caches the relevant parameters of a movement-modifier zone so the agent mover system can apply them without re-querying the entity each frame.

**Use-case:** Stored in `InsideMovementModAreaComponent.Areas` by the movement-mod system when the agent enters a zone; read by `AgentMoverSystem` to adjust speed and slide forces.

### ⭐ Constructors
```csharp
public AreaInfo(MovementModAreaComponent area)
```

Creates an `AreaInfo` snapshot from the given movement-modifier area component.

**Parameters** \
`area` [MovementModAreaComponent](../../Murder/Components/MovementModAreaComponent.html) \

### ⭐ Properties
#### Orientation
```csharp
public readonly Orientation Orientation;
```

The axis along which the slide force is applied (horizontal, vertical, or both).

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \
#### Slide
```csharp
public readonly float Slide;
```

Strength and direction of the lateral force pushed onto the agent while inside this area.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### SpeedMultiplier
```csharp
public readonly float SpeedMultiplier;
```

Factor by which the agent's speed is multiplied while inside this area; values below `1.0` slow the agent down.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡
# AreaInfo

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
sealed struct AreaInfo
```

Snapshot of the movement-modifying properties of a [MovementModAreaComponent](../../Murder/Components/MovementModAreaComponent.html) zone that an agent is currently inside, tagged with the ID of the zone entity it was copied from.

**Intent:** Caches the relevant parameters of a movement-modifier zone (speed multiplier, slide, orientation) alongside the zone entity's ID, so `AgentMoverSystem` can apply per-zone effects to an agent's velocity without re-querying the zone entity every frame, and so an agent tracking multiple overlapping zones can tell them apart by `AreaEntityId`.

**Use-case:** Stored in `InsideMovementModAreaComponent.Areas` — the movement-mod system calls `AddArea`/`RemoveArea` on that component as an agent enters or exits a `MovementModAreaComponent` zone, snapshotting the zone's data into an `AreaInfo`. `AgentMoverSystem.GetVelocity` reads `InsideMovementModAreaComponent.GetLatest()` to pull the most recently entered zone's `SpeedMultiplier`/`Slide`/`Orientation` and blend it into the agent's final impulse.

### ⭐ Constructors

```csharp
public AreaInfo(int areaEntityId, MovementModAreaComponent area)
```

Creates a snapshot from a `MovementModAreaComponent` zone entity, copying its `SpeedMultiplier`, `Orientation`, and `Slide` alongside the zone entity's ID.

**Parameters** \
`areaEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`area` [MovementModAreaComponent](../../Murder/Components/MovementModAreaComponent.html) \

```csharp
public AreaInfo(int areaEntityId, float multiplier)
```

Creates a minimal snapshot directly from a speed multiplier value (with `Orientation.Both` and no slide), without needing an actual `MovementModAreaComponent` instance.

**Parameters** \
`areaEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`multiplier` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### AreaEntityId

```csharp
public readonly int AreaEntityId;
```

Entity ID of the `MovementModAreaComponent` zone this snapshot was copied from; defaults to `-1`. `InsideMovementModAreaComponent.AddArea`/`RemoveArea` use this to identify which tracked area a given `AreaInfo` corresponds to.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SpeedMultiplier

```csharp
public readonly float SpeedMultiplier;
```

Factor by which the agent's speed is multiplied while inside this area; values below `1.0` slow the agent down, above `1.0` speed it up.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

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

⚡

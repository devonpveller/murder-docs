# InsideMovementModAreaComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InsideMovementModAreaComponent : IComponent
```

Runtime-only component that tracks every [MovementModAreaComponent](../../Murder/Components/MovementModAreaComponent.html) zone the entity is currently overlapping.

**Intent:** Record that an agent is inside one or more movement-modifier area zones so the movement system can combine every active area's speed multiplier and slide into the agent's final velocity, instead of only reacting to a single overlapping area.

**Use-case:** Added, updated and removed automatically by the agent movement-modifier system as the entity enters and exits area triggers; the agent mover system reads `Areas` each frame to apply the combined movement modifiers to the agent's velocity. Game code does not usually construct this directly — use `AddArea`/`RemoveArea` if you need to manipulate it manually.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public InsideMovementModAreaComponent(int areaEntityId, MovementModAreaComponent area)
```

Creates a component tracking a single area, identified by the area entity's id and its `MovementModAreaComponent` configuration.

**Parameters** \
`areaEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`area` [MovementModAreaComponent](../../Murder/Components/MovementModAreaComponent.html) \

```csharp
public InsideMovementModAreaComponent(AreaInfo info)
```

Creates a component tracking a single area from an already-built `AreaInfo`.

**Parameters** \
`info` [AreaInfo](../../Murder/Components/AreaInfo.html) \

```csharp
public InsideMovementModAreaComponent(ImmutableArray<AreaInfo> areas)
```

Creates a component tracking an explicit set of areas.

**Parameters** \
`areas` [ImmutableArray\<AreaInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties

#### Areas

```csharp
public readonly ImmutableArray<AreaInfo> Areas;
```

One entry per movement-modifier area the entity is currently inside, keyed by the area entity's id.

**Returns** \
[ImmutableArray\<AreaInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### AddArea(AreaInfo)

```csharp
public InsideMovementModAreaComponent AddArea(AreaInfo info)
```

Returns a new component including `info` in `Areas`. If an area with the same area entity id is already tracked, returns this instance unchanged (no-op), so it is safe to call every frame while the entity remains inside the area.

**Parameters** \
`info` [AreaInfo](../../Murder/Components/AreaInfo.html) \

**Returns** \
[InsideMovementModAreaComponent](../../Murder/Components/InsideMovementModAreaComponent.html) \

#### AddArea(int, MovementModAreaComponent)

```csharp
public InsideMovementModAreaComponent AddArea(int areaEntityId, MovementModAreaComponent area)
```

Convenience overload of `AddArea(AreaInfo)` that builds the `AreaInfo` from the area entity's id and its `MovementModAreaComponent`.

**Parameters** \
`areaEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`area` [MovementModAreaComponent](../../Murder/Components/MovementModAreaComponent.html) \

**Returns** \
[InsideMovementModAreaComponent](../../Murder/Components/InsideMovementModAreaComponent.html) \

#### RemoveArea(AreaInfo)

```csharp
public InsideMovementModAreaComponent? RemoveArea(AreaInfo info)
```

Returns a new component with the area matching `info`'s area entity id removed from `Areas`, or `null` if removing it would leave the component tracking zero areas — callers should interpret a `null` result as "remove this component from the entity entirely" rather than attaching an empty one.

**Parameters** \
`info` [AreaInfo](../../Murder/Components/AreaInfo.html) \

**Returns** \
[InsideMovementModAreaComponent](../../Murder/Components/InsideMovementModAreaComponent.html)? \

#### RemoveArea(int, MovementModAreaComponent)

```csharp
public InsideMovementModAreaComponent? RemoveArea(int areaEntityId, MovementModAreaComponent area)
```

Convenience overload of `RemoveArea(AreaInfo)` that builds the `AreaInfo` from the area entity's id and its `MovementModAreaComponent`.

**Parameters** \
`areaEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`area` [MovementModAreaComponent](../../Murder/Components/MovementModAreaComponent.html) \

**Returns** \
[InsideMovementModAreaComponent](../../Murder/Components/InsideMovementModAreaComponent.html)? \

#### GetLatest()

```csharp
public AreaInfo? GetLatest()
```

Returns the most recently added area the entity is inside, or `null` if it is not inside any area. Used by systems that only want the single most relevant modifier (e.g. the last area entered) rather than combining every overlapping area.

**Returns** \
[AreaInfo](../../Murder/Components/AreaInfo.html)? \

⚡

# InsideGravityWellComponent

**Namespace:** Murder.Components.Agents \
**Assembly:** Murder.dll

```csharp
public sealed struct InsideGravityWellComponent : IComponent
```

Marks an entity as currently standing inside the influence area of a "gravity well" entity — one that pulls or holds other entities towards it (e.g. a black-hole hazard, a magnet, a whirlpool).

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Lets the friction system distinguish velocity caused by a pulling force from ordinary movement. `FrictionSystem` checks for this component before dampening an entity's velocity: while inside a gravity well, velocity pointing towards the well referenced by `GravityWellId` is not reduced by friction, so the entity keeps being drawn in rather than sliding to a stop as friction would normally cause.

**Use-case:** Intended to be added and removed by whichever system implements the actual gravity-well area-of-effect detection (typically a trigger/collision system watching for entities entering and leaving the well's collider), not authored by hand on a prefab. When building a new "pulling hazard" feature, add this component to affected entities while they remain inside the well's range, and remove it when they leave.

### ⭐ Constructors

```csharp
public InsideGravityWellComponent(int id)
```

Marks the entity as being inside the gravity well identified by `id`.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) — the entity id of the gravity well. \

### ⭐ Properties

#### GravityWellId

```csharp
public readonly int GravityWellId;
```

The entity id of the gravity well entity this agent is currently affected by, used to look up the well's position so the friction exemption can be computed relative to it. Defaults to `-1` when unset.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

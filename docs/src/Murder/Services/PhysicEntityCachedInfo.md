# PhysicEntityCachedInfo

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public readonly struct PhysicEntityCachedInfo
```

A lightweight, value-type snapshot of an entity's collision-relevant state (id, scale, global position, and `ColliderComponent`). Declared as a nested type of [PhysicsServices](../../Murder/Services/PhysicsServices.html).

**Intent:** Physics/collision queries in `PhysicsServices` (e.g. `GetMtvAt`, `GetFirstMtv`, `CollidesAt`, and the various `FilterPositionAndColliderEntities` overloads) need to test many candidate entities against each other repeatedly within a single query. Re-fetching `PositionComponent`/`ScaleComponent`/`ColliderComponent` from each `Entity` on every comparison would be wasteful, so callers pre-extract this data once per entity into a `PhysicEntityCachedInfo` and pass a collection of them around instead of raw entities.

**Use-case:** You typically don't construct this directly — call one of `PhysicsServices.FilterPositionAndColliderEntities` to build a `List<PhysicEntityCachedInfo>` from a set of candidate entities (filtered by collision layer mask), then pass that list into `GetMtvAt`, `GetFirstMtv`, or `CollidesAt` for the actual overlap/minimum-translation-vector resolution.

### ⭐ Constructors

```csharp
public PhysicEntityCachedInfo(int entityId, Vector2 scale, Point globalPosition, ColliderComponent collider)
```

Captures a snapshot of `entityId`'s current `scale`, `globalPosition`, and `collider` at the time of construction, decoupling later collision checks from the live, possibly-changing entity state.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`globalPosition` [Point](../../Murder/Core/Geometry/Point.html) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \

### ⭐ Properties

#### Collider

```csharp
public readonly ColliderComponent Collider;
```

The snapshotted `ColliderComponent`, whose shapes are tested against other entities' colliders during a physics query.

**Returns** \
[ColliderComponent](../../Murder/Components/ColliderComponent.html) \

#### EntityId

```csharp
public readonly int EntityId;
```

The id of the entity this snapshot was captured from, used to identify which entity a collision result refers to and to exclude an entity from colliding with itself.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GlobalPosition

```csharp
public readonly Point GlobalPosition;
```

The entity's world-space position at snapshot time, used together with `Collider` and `Scale` to compute its bounding box/shapes for overlap tests.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Scale

```csharp
public readonly Vector2 Scale;
```

The entity's scale at snapshot time, applied when computing the collider's effective bounding box.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

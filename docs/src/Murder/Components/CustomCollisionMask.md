# CustomCollisionMask

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct CustomCollisionMask : IComponent
```

Overrides the default collision layer mask used when testing this entity against the physics world.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Lets individual entities opt into a non-default set of collision layers without affecting any other entity.

**Use-case:** Attach to a moving entity (anything with `PositionComponent` and `VelocityComponent`, processed by `SATPhysicsSystem`) whose movement should be blocked by a different set of layers than the engine default (`CollisionLayersBase.SOLID | CollisionLayersBase.HOLE`); set `CollisionMask` to the desired `CollisionLayersBase` flag combination. Without this component, `SATPhysicsSystem` falls back to the default mask.

### ⭐ Constructors

```csharp
public CustomCollisionMask()
```

```csharp
public CustomCollisionMask(int collisionMask)
```

**Parameters** \
`collisionMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### CollisionMask

```csharp
public readonly int CollisionMask;
```

Bitmask of `CollisionLayersBase` flags that this entity tests against during physics queries.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

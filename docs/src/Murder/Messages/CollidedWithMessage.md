# CollidedWithMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct CollidedWithMessage : IMessage
```

Carries the identity and collision layer of the other entity involved in a physical collision.

**Intent:** Notify an entity that it has physically collided with another specific entity.

**Use-case:** `SATPhysicsSystem` sends this (`e.SendCollidedWithMessage(hitId, hitLayer)`) to a moving entity whenever its swept collision check finds a solid collider it can't pass through, right before it stops or slides along the surface. Gameplay systems that need to react to hard collisions — such as `DestroyOnCollisionSystem`, which listens for it on entities with a `DestroyOnCollisionComponent` and either destroys the entity or sends a `FatalDamageMessage` depending on `KillInstead` — listen for it with `[Messager(typeof(CollidedWithMessage))]` and inspect `EntityId`/`Layer` to decide how to react.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors

```csharp
public CollidedWithMessage(int entityId, int layer)
```

Signals a collision with another entity, identifying which entity was hit and on which collision layer.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`layer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### EntityId

```csharp
public readonly int EntityId;
```

Entity ID of the other entity involved in the collision.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Layer

```csharp
public readonly int Layer;
```

Collision layer of the other entity's collider at the time of the collision.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

# OnCollisionMessage

**Namespace:** Murder.Messages.Physics \
**Assembly:** Murder.dll

```csharp
public sealed struct OnCollisionMessage : IMessage
```

Message sent to the actor entity when it touches a trigger area, carrying the other entity's ID and the direction of the collision movement.

**Intent:** Notify the actor entity that it has entered or is overlapping a trigger collider, and convey the relative movement direction.

**Use-case:** Send this from the physics/collision system to the entity that is physically moving into a trigger. Listening systems can use `EntityId` to identify the trigger zone and `Movement` to determine entry or exit direction, enabling area-specific effects such as entering a door hitbox or stepping on a pressure plate.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public OnCollisionMessage(int triggerId, CollisionDirection movement)
```

Creates a message identifying the trigger entity and the direction of movement during the collision.

**Parameters** \
`triggerId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`movement` [CollisionDirection](../../Murder/Utilities/CollisionDirection.html) \

### ⭐ Properties
#### EntityId
```csharp
public readonly int EntityId;
```

Entity ID of the trigger collider the actor has touched. Note: the entity may no longer be active when this message is processed.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Movement
```csharp
public readonly CollisionDirection Movement;
```

The direction of the actor's movement relative to the trigger area at the moment of collision.

**Returns** \
[CollisionDirection](../../Murder/Utilities/CollisionDirection.html) \


⚡
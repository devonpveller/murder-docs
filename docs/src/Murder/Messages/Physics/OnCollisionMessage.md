# OnCollisionMessage

**Namespace:** Murder.Messages.Physics \
**Assembly:** Murder.dll

```csharp
public sealed struct OnCollisionMessage : IMessage
```

Message sent to the ACTOR when touching a trigger area.

**Intent:** Bang message sent to an actor entity when it touches a trigger collider.

**Use-case:** Listen for this message on entities with collision components to react to overlap events (e.g., entering doors, pick-up areas).

**Implements:** _[IMessage](../../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public OnCollisionMessage(int triggerId, CollisionDirection movement)
```

Message sent to the ACTOR when touching a trigger area.

**Parameters** \
`triggerId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`movement` [CollisionDirection](../../../Murder/Utilities/CollisionDirection.html) \

### ⭐ Properties
#### EntityId
```csharp
public readonly int EntityId;
```

The entity ID of the trigger or collider that was touched.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Movement
```csharp
public readonly CollisionDirection Movement;
```

The direction of movement relative to the collision.

**Returns** \
[CollisionDirection](../../../Murder/Utilities/CollisionDirection.html) \


⚡
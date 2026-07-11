# CollidedWithMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct CollidedWithMessage : IMessage
```

Carries the identity and collision layer of the other entity involved in a physical collision.

**Intent:** Notify an entity that it has physically collided with another specific entity.

**Use-case:** Send this from a physics or collision detection system and receive it in gameplay systems that need to react to collisions—such as dealing damage, triggering pickups, or applying knockback—while knowing which entity and which collision layer was involved.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public CollidedWithMessage(int entityId, int layer)
```

Signals a collision with another entity

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\
`layer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

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
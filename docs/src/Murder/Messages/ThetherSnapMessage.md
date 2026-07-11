# ThetherSnapMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct ThetherSnapMessage : IMessage
```

Sent when an entity has been snapped or attached to a tether point, carrying the ID of the newly attached entity.

**Intent:** Notify relevant systems that an entity has been bound to a tether, enabling constraint-based movement or physics responses.

**Use-case:** Send this from a tether system when an entity snaps to a tether anchor. Listening systems can use the `AttachedEntityId` to apply movement constraints, synchronize animations, or trigger gameplay events tied to the attachment.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public ThetherSnapMessage(int attachedEntityId)
```

Creates a message identifying the entity that was just attached to the tether.

**Parameters** \
`attachedEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### AttachedEntityId
```csharp
public readonly int AttachedEntityId;
```

Entity ID of the entity that has been attached to this tether.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
# ThetherSnapMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct ThetherSnapMessage : IMessage
```

Sent when an entity has been snapped or attached to a tether point, carrying the ID of the newly attached entity. Note: the type name itself has this "Thether" spelling in the engine source (not a documentation typo).

**Intent:** Notify relevant systems that an entity has been bound to a tether, enabling constraint-based movement or physics responses.

**Use-case:** No built-in engine system currently sends or listens for this message (it has no callers under `src/Murder`); it exists as a ready-made message type for game-specific tether systems to send when an entity snaps to a tether anchor. Listening systems can use `AttachedEntityId` to apply movement constraints, synchronize animations, or trigger gameplay events tied to the attachment.

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

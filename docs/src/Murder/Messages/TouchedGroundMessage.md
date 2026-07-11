# TouchedGroundMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct TouchedGroundMessage : IMessage
```

A marker message with no payload sent when a falling or airborne entity first makes contact with the ground.

**Intent:** Notify systems that an entity has landed, enabling ground-contact reactions.

**Use-case:** Send this from a physics or movement system when vertical velocity transitions from falling to grounded. Listening systems can play landing sound effects, trigger dust particle effects, reset jump counters, or apply landing-impact logic.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public TouchedGroundMessage()
```

Creates a ground-contact notification with no additional data.


⚡
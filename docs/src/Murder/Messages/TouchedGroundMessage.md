# TouchedGroundMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct TouchedGroundMessage : IMessage
```

A marker message with no payload sent every fixed tick that an entity with a `VerticalPositionComponent` has its simulated height (`Z`) at ground level, not just on the first frame of contact.

**Intent:** Notify systems that an entity is currently resting on/touching the ground (as opposed to airborne), enabling ground-contact reactions.

**Use-case:** `VerticalPhysicsSystem.FixedUpdate` sends this (`e.SendTouchedGroundMessage()`) every fixed tick that `verticalPosition.Z == 0`, for as long as the entity keeps a `VerticalPositionComponent` — which is removed only once `ZVelocity` also settles to zero (bouncing has fully stopped). Because it repeats while grounded rather than firing once, a `[Messager(typeof(TouchedGroundMessage))]` listener that wants a one-shot "landed" reaction (a sound effect, a dust particle burst, resetting a jump counter) should guard against re-triggering every tick, e.g. by checking/setting a flag component the first time it's received.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors

```csharp
public TouchedGroundMessage()
```

Creates a ground-contact notification with no additional data.

⚡

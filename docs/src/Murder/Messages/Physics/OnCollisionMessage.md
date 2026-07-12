# OnCollisionMessage

**Namespace:** Murder.Messages.Physics \
**Assembly:** Murder.dll

```csharp
public sealed struct OnCollisionMessage : IMessage
```

Message reporting a trigger-collider overlap between two entities, sent to **both** entities involved (not just one side), carrying the other entity's ID and whether this is an enter or exit event.

**Intent:** Give any listener on either side of a trigger overlap (the trigger itself, or the actor/hitbox that entered it) a single message type to react to, without needing to poll collider state or care which side it is.

**Use-case:** `TriggerPhysicsSystem` is the sole producer: it tracks `ACTOR`/`HITBOX` colliders overlapping `TRIGGER` colliders and, on every enter/exit transition, sends this message to *both* the trigger entity and the actor entity via its private `SendCollisionMessages` helper (`actor.SendOnCollisionMessage(...)` and `trigger.SendOnCollisionMessage(...)`). Listen for it with `[Messager(typeof(OnCollisionMessage))]`; for example `InteractOnCollisionSystem` uses it (together with an `InteractOnCollisionComponent`) to fire an `InteractMessage` at the other entity once an agent enters a trigger, and `AgentMovementModfierSystem`/`AmbienceTrackerSystem` use it to apply or remove movement modifiers and ambience zones as agents step in and out of trigger areas. Use `EntityId` to look up the other entity (it may already be destroyed/inactive by the time the message is processed) and `Movement` to branch on entering vs. leaving.

**Implements:** _[IMessage](../../../Bang/Components/IMessage.html)_

### ⭐ Constructors

```csharp
public OnCollisionMessage(int triggerId, CollisionDirection movement)
```

Creates a message identifying the other entity involved in the overlap and whether the overlap is starting or ending. Despite the parameter name `triggerId`, this constructor is used for the message sent to either side of the collision (the trigger's message carries the actor's ID, and the actor's message carries the trigger's ID).

**Parameters** \
`triggerId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`movement` [CollisionDirection](../../../Murder/Utilities/CollisionDirection.html) \

### ⭐ Properties

#### EntityId

```csharp
public readonly int EntityId;
```

Entity ID of the other entity on the opposite side of the trigger overlap. Be aware that entity may no longer exist or be active by the time this message is handled (e.g. it was destroyed the same frame).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Movement

```csharp
public readonly CollisionDirection Movement;
```

Whether the other entity just entered (`CollisionDirection.Enter`) or exited (`CollisionDirection.Exit`) the trigger overlap.

**Returns** \
[CollisionDirection](../../../Murder/Utilities/CollisionDirection.html) \

⚡

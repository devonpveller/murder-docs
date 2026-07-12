# EventBroadcasterSystem

**Namespace:** Murder.Systems.Effects \
**Assembly:** Murder.dll

```csharp
public class EventBroadcasterSystem : IMessagerSystem, ISystem
```

Forwards an `AnimationEventMessage` received on an entity to one of its children, instead of handling the event itself.

**Intent:** Lets a composite entity re-route animation events to the specific child that should actually react to them, when the sprite that owns the animation (and therefore fires the event) is a different entity than the one whose `EventListenerComponent` should respond.

**Use-case:** Add `BroadcastEventMessageComponent` to a parent/rig entity with `Target` set to the child id that should receive the event. When the parent receives an `AnimationEventMessage`, this system re-sends the same message to that child, where [EventListenerSystem](EventListenerSystem.html) (or another `EventBroadcasterSystem`, allowing chained forwarding) can pick it up. Entities with `MuteEventsComponent` are excluded from this system entirely.

**Implements:** _[IMessagerSystem](../../../Bang/Systems/IMessagerSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public EventBroadcasterSystem()
```

### ⭐ Methods

#### OnMessage(World, Entity, IMessage)

```csharp
public virtual void OnMessage(World world, Entity entity, IMessage message)
```

Re-sends the received `AnimationEventMessage` to the child entity identified by this entity's `BroadcastEventMessageComponent.Target`, if that child currently exists.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entity` [Entity](../../../Bang/Entities/Entity.html) \
`message` [IMessage](../../../Bang/Components/IMessage.html) \

⚡

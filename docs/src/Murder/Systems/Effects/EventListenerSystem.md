# EventListenerSystem

**Namespace:** Murder.Systems.Effects \
**Assembly:** Murder.dll

```csharp
public class EventListenerSystem : IMessagerSystem, ISystem
```

Processes entities with `EventListenerComponent`, invoking registered callbacks when a matching Bang message is received.

**Intent:** Dispatches Bang messages to per-entity event listener callbacks.

**Use-case:** Include in any world where entities use `EventListenerComponent` to register named callbacks that fire in response to specific message types.

**Implements:** _[IMessagerSystem](../../../Bang/Systems/IMessagerSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public EventListenerSystem()
```

### ⭐ Methods
#### OnMessage(World, Entity, IMessage)
```csharp
public virtual void OnMessage(World world, Entity entity, IMessage message)
```

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entity` [Entity](../../../Bang/Entities/Entity.html) \
`message` [IMessage](../../../Bang/Components/IMessage.html) \



⚡
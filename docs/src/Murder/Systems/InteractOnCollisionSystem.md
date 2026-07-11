# InteractOnCollisionSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class InteractOnCollisionSystem : IMessagerSystem, ISystem
```

Interactors tag hightlights and interacts with InteractorComponents

**Intent:** Triggers interaction logic when a colliding entity (e.g., the player) enters or exits the bounds of an interactive entity.

**Use-case:** Attach `InteractOnCollisionComponent` to doors, pickups, or trigger zones; this system routes `OnCollisionMessage` events to the entity's interaction handlers automatically.

**Implements:** _[IMessagerSystem](../../Bang/Systems/IMessagerSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public InteractOnCollisionSystem()
```

### ⭐ Methods
#### IsInteractAllowed(Entity, InteractOnCollisionComponent)
```csharp
protected virtual bool IsInteractAllowed(Entity interactor, InteractOnCollisionComponent component)
```

Override to add custom conditions that must be satisfied before an interaction is allowed to fire; returns `true` by default.

**Parameters** \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`component` [InteractOnCollisionComponent](../../Murder/Components/InteractOnCollisionComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### OnMessage(World, Entity, IMessage)
```csharp
public virtual void OnMessage(World world, Entity entity, IMessage message)
```

**Parameters** \
`world` [World](../../Bang/World.html) \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`message` [IMessage](../../Bang/Components/IMessage.html) \



⚡
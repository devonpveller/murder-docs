# AddChildOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct AddChildOnInteraction : IInteraction
```

This will set up a landing plot by adding a child to it.

**Intent:** Spawns a configured prefab as a named child of the interacted entity.

**Use-case:** Use when interacting with an entity should dynamically attach a child prefab to it, such as equipping an item, spawning a held object, or adding a visual sub-entity.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public AddChildOnInteraction()
```

### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Instantiates the configured prefab and attaches it as a named child of the interacted entity, optionally forwarding the child's event listener data to the parent.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
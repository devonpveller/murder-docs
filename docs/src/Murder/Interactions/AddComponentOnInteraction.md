# AddComponentOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct AddComponentOnInteraction : IInteraction
```

This will trigger an effect by placing [AddComponentOnInteraction.Component](../../Murder/Interactions/AddComponentOnInteraction.html#component) in the world.

**Intent:** Adds or replaces a component on a target entity when the interaction fires.

**Use-case:** Use to toggle behaviour on an entity at interaction time, for example adding a `FreezeWorldComponent`, a visual highlight, or a state component to the interacted entity, its parent, or the interactor.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Properties
#### Component
```csharp
public readonly IComponent Component;
```
The component instance that will be added or replaced on the target entity.

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \
#### Target
```csharp
public readonly TargetEntity Target;
```
Determines which entity receives the component: the interacted entity itself, its parent, or the interactor.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Adds or replaces `Component` on the entity selected by `Target`, safely deep-copying modifiable components.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
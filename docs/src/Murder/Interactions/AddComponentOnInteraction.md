# AddComponentOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct AddComponentOnInteraction : IInteraction
```

Adds (or replaces) [Component](../../Murder/Interactions/AddComponentOnInteraction.html#component) on whichever entity `Target` resolves to when the interaction fires.

**Intent:** General-purpose way to attach arbitrary gameplay state/behaviour to an entity as a side-effect of an interaction, without a dedicated interaction type for every component.

**Use-case:** Use to toggle behaviour on an entity at interaction time — for example tagging the interacted entity with a status-effect component, marking the interactor with a flag component, adding a component to a resolved "Target" entity, or spawning a brand new child entity that only carries the given component.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Properties

#### Component

```csharp
public readonly IComponent Component;
```

The component instance to add (or replace, if the target entity already has a component of the same type) on the resolved target entity. If this is an `IModifiableComponent`, it is deep-copied before being attached so the same serialized instance can safely be reused across multiple interactions/entities.

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \

#### Target

```csharp
public readonly TargetEntity Target;
```

Selects which entity receives `Component`: the interacted entity itself, its parent, the interactor, an entity referenced via `Target`/`IdTargetCollection`, a brand new child entity, or a named child.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Adds or replaces `Component` on the entity selected by `Target`, safely deep-copying modifiable components before attaching them.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡

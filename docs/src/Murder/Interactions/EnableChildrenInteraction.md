# EnableChildrenInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct EnableChildrenInteraction : IInteraction
```

Activates all inactive child entities of the interacted entity (or a specified target) when the interaction fires.

**Intent:** Enables hidden child entities so they become visible and active in the world.

**Use-case:** Use to reveal children on interaction, such as making a door open by activating its open-state child sprites, or revealing hidden items under an entity.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Activates all inactive children of the interacted entity, or of the entity resolved via the optional target name.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

#### Enable(World, Entity)
```csharp
public void Enable(World world, Entity target)
```
Activates all inactive children of `target`, resetting their animation start time if they have a sprite component.

**Parameters** \
`world` [World](../../Bang/World.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \



⚡
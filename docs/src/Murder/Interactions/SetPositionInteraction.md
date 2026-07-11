# SetPositionInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SetPositionInteraction : IInteraction
```

Moves the interacted entity to an absolute world position when the interaction fires.

**Intent:** Teleports or repositions an entity to a fixed coordinate in the world.

**Use-case:** Use to snap an entity to a predetermined location, such as a respawn point or a scripted placement position during a cutscene.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public SetPositionInteraction()
```

### ⭐ Properties
#### Position
```csharp
public readonly Point Position;
```
The absolute world coordinate the interacted entity will be moved to.

**Returns** \
[Point](https://docs.monogame.net/api/Microsoft.Xna.Framework.Point.html) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Sets the global position of the interacted entity to `Position`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
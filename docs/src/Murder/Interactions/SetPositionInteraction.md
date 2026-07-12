# SetPositionInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SetPositionInteraction : IInteraction
```

Moves the interacted entity to an absolute world position when the interaction fires.

**Intent:** Teleports or repositions an entity to a fixed coordinate in the world.

**Use-case:** Use for scripted placements such as snapping the player to a respawn point, moving a prop into position for a cutscene, or relocating an entity through a door/portal trigger.

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

The absolute world coordinate (in tile/pixel space) the interacted entity will be moved to.

**Returns** \
[Point](https://docs.monogame.net/api/Microsoft.Xna.Framework.Point.html) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Sets the global position of `interacted` to `Position`. Does nothing if `interacted` is `null`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡

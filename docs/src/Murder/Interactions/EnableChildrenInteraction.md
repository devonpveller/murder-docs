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

### ⭐ Constructors

```csharp
public EnableChildrenInteraction()
```

### ⭐ Properties

#### Target

```csharp
public readonly string? Target;
```

Optional name of a target entity (resolved the same way as other target-decorated fields, via the interacted entity's target components) whose children should be activated instead of the interacted entity's own children. When `null`, the interacted entity's own children are used.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Activates all inactive children of the interacted entity, or of the entity resolved via `Target`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

#### Enable(World, Entity)

```csharp
public static void Enable(World world, Entity target)
```

Activates all inactive children of `target`, resetting their animation start time if they have a sprite component so the animation plays from the beginning instead of appearing mid-animation.

**Parameters** \
`world` [World](../../Bang/World.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \

⚡

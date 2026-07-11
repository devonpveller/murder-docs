# PlaySoundInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct PlaySoundInteraction : IInteraction
```

Plays a one-shot or looping sound event when the interaction fires.

**Intent:** Triggers a sound effect in response to an in-world interaction.

**Use-case:** Use to play a door creak, button click, or ambient sound cue whenever a player or entity activates an interactive object.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public PlaySoundInteraction()
```

### ⭐ Properties
#### Sound
```csharp
public readonly SoundEventId Sound;
```
The sound event identifier of the effect to play.

**Returns** \
[SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Plays the configured sound event via `SoundServices`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
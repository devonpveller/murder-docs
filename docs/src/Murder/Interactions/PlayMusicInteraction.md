# PlayMusicInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct PlayMusicInteraction : IInteraction
```

Starts a music event when the interaction fires, optionally stopping a previous track.

**Intent:** Triggers a background music transition as a result of an in-world interaction.

**Use-case:** Use to change the background music when the player enters a new area or triggers a scripted event, such as switching from an exploration theme to a combat theme.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public PlayMusicInteraction()
```

### ⭐ Properties
#### Music
```csharp
public readonly SoundEventId Music;
```
The sound event identifier of the music track to start playing.

**Returns** \
[SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
#### PreviousMusic
```csharp
public readonly T? PreviousMusic;
```
Optional identifier of the previous music track to restore after this one ends, if applicable.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### StopPrevious
```csharp
public readonly bool StopPrevious;
```
When `true`, stops the currently playing music before starting the new track.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Plays `Music`, optionally stopping the previous track first.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
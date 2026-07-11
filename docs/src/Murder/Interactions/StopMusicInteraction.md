# StopMusicInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct StopMusicInteraction : IInteraction
```

Stops one or all playing music events when the interaction fires.

**Intent:** Halts background music (with optional fade-out) as part of an in-world interaction.

**Use-case:** Use to silence music at a dramatic moment, transition to silence before a cutscene, or stop a specific music layer when the player leaves an area.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public StopMusicInteraction()
```

### ⭐ Properties
#### ExceptFor
```csharp
public readonly T? ExceptFor;
```

TODO: We might replace this with a "category" of sounds we want to exclude/include in the stop.
            I will wait until we need that first.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### FadeOut
```csharp
public readonly bool FadeOut;
```
When `true`, the music fades out gradually instead of stopping abruptly.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Music
```csharp
public readonly T? Music;
```
The specific music event to stop; when `null`, all currently playing music events are stopped (except those listed in `ExceptFor`).

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Stops the configured music event (or all events), optionally fading out.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
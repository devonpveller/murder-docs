# MusicComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct MusicComponent : IComponent
```

Music component which will be immediately played and destroyed.

**Intent:** Trigger background music playback on an entity; the sound system plays the specified event and then disposes of the component.

**Use-case:** Add to any entity (or a dedicated music entity) with the desired `SoundEventId` to start a music track; remove the component or use a dedicated stop interaction to silence it.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public MusicComponent()
```

```csharp
public MusicComponent(SoundEventId id)
```

**Parameters** \
`id` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \

### ⭐ Properties
#### Id
```csharp
public readonly SoundEventId Id;
```

Identifier of the sound event (music track) to play.

**Returns** \
[SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \


⚡
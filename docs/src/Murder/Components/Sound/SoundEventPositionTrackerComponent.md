# SoundEventPositionTrackerComponent

**Namespace:** Murder.Components.Sound \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundEventPositionTrackerComponent : IComponent
```

This will track the spatial position of an event.

**Intent:** Keep a sound event's 3D position synchronised with the entity's world position each frame.

**Use-case:** Attach to an entity that emits a positional audio event so the audio engine receives updated coordinates as the entity moves.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public SoundEventPositionTrackerComponent(SoundEventId sound)
```

**Parameters** \
`sound` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

### ⭐ Properties
#### Sound
```csharp
public readonly SoundEventId Sound;
```

Identifier of the sound event whose spatial position is being tracked.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \


⚡
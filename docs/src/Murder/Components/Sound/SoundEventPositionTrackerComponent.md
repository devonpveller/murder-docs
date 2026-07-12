# SoundEventPositionTrackerComponent

**Namespace:** Murder.Components.Sound \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundEventPositionTrackerComponent : IComponent
```

Marks that a sound event is currently playing and spatially attached to this entity, so its emitter position keeps following the entity every frame.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** `SoundEventPositionTrackerSystem` runs once per frame over every entity carrying this component and calls `SoundServices.TrackEventSourcePosition` with `Sound` and the entity, updating the underlying audio engine's emitter position to match the entity's current world position.

**Use-case:** This is added automatically by systems that start a positional sound tied to an entity and need to keep it moving with that entity — for example, the agent footstep-sound tracker (`AgentOnMoveTrackerComponent`'s companion system) sets this when it starts the walk sound, and removes it when the sound stops. It is not intended to be authored by hand on a prefab; add it programmatically right after starting a positional sound event on an entity that will keep moving.

### ⭐ Constructors

```csharp
public SoundEventPositionTrackerComponent(SoundEventId sound)
```

Creates the tracker for the given sound event, which is expected to already be playing.

**Parameters** \
`sound` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) — identifier of the sound event to keep spatially updated. \

### ⭐ Properties

#### Sound

```csharp
public readonly SoundEventId Sound;
```

Identifier of the currently playing sound event whose spatial position is kept in sync with this entity's world position.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

⚡

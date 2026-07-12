# AgentOnMoveTrackerComponent

**Namespace:** Murder.Components.Agents \
**Assembly:** Murder.dll

```csharp
public sealed struct AgentOnMoveTrackerComponent : IComponent
```

Drives a looping "footstep"-style sound event that follows an agent's movement state, playing while the agent is moving and stopping (with a fade-out) once it's idle.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Ties a positional sound event's playback directly to whether an entity is currently moving, without requiring bespoke gameplay code. A companion system inside `AgentMoverSystem` (the reactive `AgentMoverSoundSystem`) watches for this component: every fixed update it checks whether the entity is moving and plays `OnWalk` if so, or stops it otherwise; it also stops the sound if the component or entity is removed or deactivated.

**Use-case:** Attach to agents that should have a continuous movement sound synced to their actual velocity — most commonly the player character's footstep loop, but also usable for NPCs, vehicles, or other moving entities that need a "while moving" sound. While playing, the tracked sound's position is kept in sync with the entity via a [SoundEventPositionTrackerComponent](../../../Murder/Components/Sound/SoundEventPositionTrackerComponent.html) that gets attached automatically.

### ⭐ Constructors

```csharp
public AgentOnMoveTrackerComponent()
```

Default constructor; `OnWalk` is left as a default (uninitialized) [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html), so no sound will actually play until a proper event is set via the other constructor.

```csharp
public AgentOnMoveTrackerComponent(SoundEventId onWalk)
```

Creates the tracker with the sound event to play while the agent is moving.

**Parameters** \
`onWalk` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) — identifier of the looping movement sound event. \

### ⭐ Properties

#### OnWalk

```csharp
public SoundEventId OnWalk { get; init; }
```

The sound event played on a loop while the agent is moving, and stopped (with a fade-out) once it stops moving, the component is removed, or the entity is deactivated.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

⚡

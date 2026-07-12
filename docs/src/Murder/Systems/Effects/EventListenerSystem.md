# EventListenerSystem

**Namespace:** Murder.Systems.Effects \
**Assembly:** Murder.dll

```csharp
public class EventListenerSystem : IMessagerSystem, ISystem
```

Dispatches sprite animation events to their configured sound and interaction handlers.

**Intent:** When a sprite's animation reaches an event frame (an Aseprite tag), the render system sends an `AnimationEventMessage`; this system looks the event name up in the entity's `EventListenerComponent` and plays the mapped sound and/or runs the mapped interaction chain.

**Use-case:** Include in any world where entities use `EventListenerComponent` (usually populated at load time from an `EventListenerEditorComponent`) to fire sounds or interactions on specific animation frames - footstep sounds, attack hitboxes, VFX triggers, etc. Playback is automatically gated by visibility: off-screen entities are skipped unless they carry `PlayEvenOffScreenComponent`, are UI, or are cutscene anchors, and invisible (alpha 0) or near-invisible entities never play. Entities with `MuteEventsComponent` are excluded entirely. Subclass and override `CanPlayFromEntity` or `OverridePlayEvent` to customize the visibility check or hook custom sound-playing logic.

**Implements:** _[IMessagerSystem](../../../Bang/Systems/IMessagerSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public EventListenerSystem()
```

### ⭐ Methods

#### CanPlayFromEntity(World, Entity)

```csharp
protected virtual bool CanPlayFromEntity(World world, Entity e)
```

Determines whether an event fired on the entity is allowed to play, for entities that aren't already exempt via `PlayEvenOffScreenComponent`, UI, or cutscene anchors. The default implementation only checks whether the entity is currently visible in the camera; override this in a subclass to add project-specific gating.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`e` [Entity](../../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### OnMessage(World, Entity, IMessage)

```csharp
public virtual void OnMessage(World world, Entity entity, IMessage message)
```

Handles the `AnimationEventMessage` for an entity: resolves the fired event name against the entity's `EventListenerComponent` and, if a match is found and the entity is allowed to play, plays the mapped sound and/or runs the mapped interactions.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entity` [Entity](../../../Bang/Entities/Entity.html) \
`message` [IMessage](../../../Bang/Components/IMessage.html) \

#### OverridePlayEvent(World, Entity, string, SoundEventId, SoundLayer, SoundProperties)

```csharp
protected virtual bool OverridePlayEvent(World world, Entity? target, string id, SoundEventId sound, SoundLayer layer, SoundProperties properties)
```

Extension point called before the default sound-playback logic runs for a resolved event sound. Return `true` to indicate the sound was already handled (e.g. played with custom parameters, redirected, or suppressed) so the default playback is skipped; the default implementation returns `false`, letting the base implementation play it normally.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`target` [Entity](../../../Bang/Entities/Entity.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`sound` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
`layer` SoundLayer \
`properties` [SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡

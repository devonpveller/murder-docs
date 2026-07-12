# SoundServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class SoundServices
```

Provides the high-level API for playing, stopping, and parameterising audio events on top of the engine's sound backend (`Game.Sound`).

**Intent:** Abstracts the audio middleware so game code can trigger and control sound events — including spatial attachment to an entity, music/snapshot layers, and per-event parameters — without depending directly on the underlying sound implementation.

**Use-case:** Use `Play` to fire a one-off sound (optionally spatially attached to an entity via its `Entity` overload), `PlayMusic`/`PlaySnapshot` for looping background layers, `Stop`/`StopAll` to silence events (e.g. on scene exit), `SetGlobalParameter`/`SetParameter` to drive FMOD-style continuous parameters (such as intensity or environment), and `TryGetSoundForEvent`/`TrackEventSourcePosition` when wiring sounds to sprite animation events.

### ⭐ Methods

#### GetGlobalParameter(ParameterId)

```csharp
public static float GetGlobalParameter(ParameterId id)
```

Returns the current value of the global sound parameter identified by `id`.

**Parameters** \
`id` [ParameterId](../../Murder/Core/Sounds/ParameterId.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetSpatialAttributes(Entity?)

```csharp
public static SoundSpatialAttributes? GetSpatialAttributes(Entity? target)
```

Builds `SoundSpatialAttributes` (position and facing direction) for playing a sound as if it came from `target`. Position is read from the root entity's (`EntityServices.FindRootEntity`) `PositionComponent`, and direction from `target.TryGetFacing()`. Returns `null` if `target` is `null`. Used internally by `Play`'s entity-targeted overload, but also useful directly when building custom sound-triggering logic.

**Parameters** \
`target` [Entity?](../../Bang/Entities/Entity.html) \

**Returns** \
[SoundSpatialAttributes?](../../Murder/Core/Sounds/SoundSpatialAttributes.html) \

#### GetSpatialAttributes(Vector2)

```csharp
public static SoundSpatialAttributes GetSpatialAttributes(Vector2 position)
```

Builds `SoundSpatialAttributes` for a sound emitted from a fixed 2D world `position` (with `Direction.Up` as a default facing), converting it to the 3D vector the sound backend expects.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[SoundSpatialAttributes](../../Murder/Core/Sounds/SoundSpatialAttributes.html) \

#### GetSpatialAttributes(Vector3)

```csharp
public static SoundSpatialAttributes GetSpatialAttributes(Vector3 position)
```

Builds `SoundSpatialAttributes` for a sound emitted from a fixed 3D `position` (with `Direction.Up` as a default facing). Used by `PlayFromListenerPosition` and `UpdateListenerPosition` to describe a fixed emission point.

**Parameters** \
`position` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

**Returns** \
[SoundSpatialAttributes](../../Murder/Core/Sounds/SoundSpatialAttributes.html) \

#### IsPlaying(SoundEventId, int)

```csharp
public static bool IsPlaying(SoundEventId eventId, int entityId)
```

Returns whether `eventId` is currently playing, attached to `entityId` (`Game.Sound.IsEventPlaying`).

**Parameters** \
`eventId` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Pause(SoundLayer)

```csharp
public static void Pause(SoundLayer layer)
```

Pauses every currently playing sound event on `layer`.

**Parameters** \
`layer` [SoundLayer](../../Murder/Core/Sounds/SoundLayer.html) \

#### Play(SoundEventId, SoundLayer, SoundProperties, SoundSpatialAttributes?, int, ParameterValue?, FireAndPersistInfo?)

```csharp
public static async ValueTask Play(SoundEventId id, SoundLayer layer = SoundLayer.Any, SoundProperties properties = SoundProperties.None, SoundSpatialAttributes? attributes = null, int entityId = -1, ParameterValue? parameter = null, FireAndPersistInfo? fireAndPersist = null)
```

The lowest-level `Play` overload; every other `Play`/`PlayMusic`/`PlaySnapshot`/`PlayFromListenerPosition` overload eventually calls this one. No-ops if `id` is an empty guid or the game is currently skipping delta-time updates. Automatically adds `SoundProperties.Persist` when `layer` is `Music` or `Snapshot`. Prefer one of the more specific overloads unless you need direct control over every parameter (spatial attributes, entity attachment, a continuous parameter, and/or fire-and-persist tracking) at once.

**Parameters** \
`id` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
`layer` [SoundLayer](../../Murder/Core/Sounds/SoundLayer.html) \
`properties` [SoundProperties](../../Murder/Core/Sounds/SoundProperties.html) \
`attributes` [SoundSpatialAttributes?](../../Murder/Core/Sounds/SoundSpatialAttributes.html) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`parameter` [ParameterValue?](../../Murder/Core/Sounds/ParameterValue.html) \
`fireAndPersist` [FireAndPersistInfo?](../../Murder/Core/Sounds/FireAndPersistInfo.html) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### Play(SoundEventId, Entity?, SoundLayer, SoundProperties)

```csharp
public static ValueTask Play(SoundEventId id, Entity? target, SoundLayer layer = SoundLayer.Any, SoundProperties properties = SoundProperties.None)
```

Plays `id`, spatially positioned using `target`'s current location and facing (via `GetSpatialAttributes(Entity?)`). This is the overload to reach for whenever a sound should appear to come from a specific entity — footsteps, hit reactions, dialogue barks, etc. Pass `target` as `null` to play without spatial attributes.

**Parameters** \
`id` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
`target` [Entity?](../../Bang/Entities/Entity.html) \
`layer` [SoundLayer](../../Murder/Core/Sounds/SoundLayer.html) \
`properties` [SoundProperties](../../Murder/Core/Sounds/SoundProperties.html) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### PlayFromListenerPosition(SoundEventId, float)

```csharp
public static ValueTask PlayFromListenerPosition(SoundEventId id, float duration = 0)
```

Plays `id` anchored at the audio listener's last known position (`Game.Sound.LastListenerPosition`), rather than at an entity or fixed point. If `duration` is greater than zero, the event is registered to fire-and-persist for that duration while following the listener's position as it moves. Useful for ambient one-shots that should always sound like they're coming from "around the camera/player" rather than a specific world position.

**Parameters** \
`id` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### PlayMusic(SoundEventId)

```csharp
public static async ValueTask PlayMusic(SoundEventId id)
```

Plays `id` on the `SoundLayer.Music` layer with `SoundProperties.Persist`, so it keeps playing across whatever normally stops one-shot sounds (e.g. scene sound cleanup) until explicitly stopped.

**Parameters** \
`id` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### PlaySnapshot(SoundEventId)

```csharp
public static async ValueTask PlaySnapshot(SoundEventId id)
```

Plays `id` on the `SoundLayer.Snapshot` layer with `SoundProperties.Persist`. Snapshots are typically used for mix-state changes (e.g. muffling ambient audio while in a menu) rather than audible one-shots.

**Parameters** \
`id` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### PlayWithParameter&lt;T&gt;(SoundEventId, Entity?, SoundLayer, SoundProperties, ParameterId, T)

```csharp
public static ValueTask PlayWithParameter<T>(SoundEventId id, Entity? target, SoundLayer layer, SoundProperties properties, ParameterId parameter, T value)
```

Plays `id` spatially attached to `target` (like `Play(SoundEventId, Entity?, SoundLayer, SoundProperties)`) while also setting a per-instance `parameter` to `value` at the moment the event starts. `value` is converted to `float` via `Convert.ToSingle`; if the conversion fails, a warning is logged and the event plays without the parameter. Use this when a sound's initial pitch/intensity/variant needs to be driven by gameplay data (e.g. impact force) rather than set globally.

**Parameters** \
`id` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
`target` [Entity?](../../Bang/Entities/Entity.html) \
`layer` [SoundLayer](../../Murder/Core/Sounds/SoundLayer.html) \
`properties` [SoundProperties](../../Murder/Core/Sounds/SoundProperties.html) \
`parameter` [ParameterId](../../Murder/Core/Sounds/ParameterId.html) \
`value` `T` \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### ReplaceIdentifiers(ImmutableDictionary&lt;string, SpriteEventInfo&gt;, Func&lt;string, string&gt;)

```csharp
public static ImmutableDictionary<string, SpriteEventInfo> ReplaceIdentifiers(ImmutableDictionary<string, SpriteEventInfo> source, Func<string, string> converter)
```

Returns a copy of the animation-event-to-sound dictionary `source` with every key run through `converter`, rebuilding each `SpriteEventInfo` under its new identifier. Used by sprite/animation editor tooling when renaming animation events so any sound-event bindings keyed by the old name are carried over to the new one.

**Parameters** \
`source` [ImmutableDictionary\<string, SpriteEventInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
`converter` [Func\<string, string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \

**Returns** \
[ImmutableDictionary\<string, SpriteEventInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### Resume(SoundLayer)

```csharp
public static void Resume(SoundLayer layer)
```

Resumes every paused sound event on `layer`.

**Parameters** \
`layer` [SoundLayer](../../Murder/Core/Sounds/SoundLayer.html) \

#### SetGlobalParameter&lt;T&gt;(ParameterId, T)

```csharp
public static void SetGlobalParameter<T>(ParameterId id, T value)
```

Sets the global sound parameter `id` to `value`, converting `value` to `float` via `Convert.ToSingle` (logging a warning and doing nothing if the conversion fails). Global parameters affect the whole mix rather than a single event instance — use this for state like overall game intensity or an environment/reverb selector.

**Parameters** \
`id` [ParameterId](../../Murder/Core/Sounds/ParameterId.html) \
`value` `T` \

#### SetParameter&lt;T&gt;(ParameterId, SoundEventId, T)

```csharp
public static void SetParameter<T>(ParameterId id, SoundEventId sound, T value)
```

Sets the parameter `id` to `value` on the currently playing instance(s) of `sound`, converting `value` to `float` via `Convert.ToSingle`. Use this to change a per-instance parameter (e.g. a footstep surface type) on a sound that's already playing, as opposed to `SetGlobalParameter` which affects the whole mix.

**Parameters** \
`id` [ParameterId](../../Murder/Core/Sounds/ParameterId.html) \
`sound` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
`value` `T` \

#### SetVolume(SoundLayer, float)

```csharp
public static void SetVolume(SoundLayer layer, float volume)
```

Immediately sets the volume of `layer` to `volume`.

**Parameters** \
`layer` [SoundLayer](../../Murder/Core/Sounds/SoundLayer.html) \
`volume` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetVolume(SoundLayer, float, float)

```csharp
public static void SetVolume(SoundLayer layer, float volume, float afterSeconds)
```

Sets the volume of `layer` to `volume`, ramping/firing after `afterSeconds`. Use this to fade a layer's volume in or out over time instead of snapping instantly.

**Parameters** \
`layer` [SoundLayer](../../Murder/Core/Sounds/SoundLayer.html) \
`volume` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`afterSeconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Stop(SoundEventId?, bool, int)

```csharp
public static void Stop(SoundEventId? id, bool fadeOut, int entityId = -1)
```

Stops the sound event identified by `id` (optionally scoped to a specific `entityId` instance), optionally fading it out instead of cutting it abruptly.

**Parameters** \
`id` [SoundEventId?](../../Murder/Core/Sounds/SoundEventId.html) \
`fadeOut` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Stop(SoundLayer, bool)

```csharp
public static void Stop(SoundLayer layer, bool fadeOut)
```

Stops every currently playing event on `layer`, optionally fading out.

**Parameters** \
`layer` [SoundLayer](../../Murder/Core/Sounds/SoundLayer.html) \
`fadeOut` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### StopAll(bool)

```csharp
public static void StopAll(bool fadeOut)
```

Stops every currently playing event on every layer (`Stop(SoundLayer.Any, fadeOut)`), optionally fading out. Typical use is clearing all audio when leaving a scene or resetting the game.

**Parameters** \
`fadeOut` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ToListenerVector3(Vector2)

```csharp
public static Vector3 ToListenerVector3(Vector2 position)
```

Converts a 2D world `position` to the 3D vector used to represent the audio listener, fixing the Z component to `1` (so the listener sits slightly in front of the 2D plane other sounds are emitted from, giving the sound backend a stable forward direction).

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### TrackEventSourcePosition(SoundEventId, Entity)

```csharp
public static void TrackEventSourcePosition(SoundEventId eventId, Entity e)
```

Updates the 3D position of an already-playing `eventId` event to follow the current position/facing of entity `e`. Call this every frame (or whenever `e` moves) for a long-running spatial sound that must track a moving entity, such as a looping engine hum attached to a vehicle.

**Parameters** \
`eventId` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### TrackEventSourcePosition(SoundEventId, int, Vector2)

```csharp
public static void TrackEventSourcePosition(SoundEventId eventId, int entityId, Vector2 position)
```

Updates the 3D position of an already-playing `eventId` event (identified by `entityId`) to `position` directly, for callers that already have a world position and don't want to look it up from an `Entity`.

**Parameters** \
`eventId` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### TryGetSoundForEvent(Entity, string)

```csharp
public static SoundEventId? TryGetSoundForEvent(Entity e, string animationEventId)
```

Looks up the sound event bound to `animationEventId` on entity `e`'s `EventListenerComponent` (checking the entity's own component first, then a child entity named `"interaction"`), returning `null` if no listener or matching event exists. Used by sprite/animation systems to trigger the correct sound when a named animation frame event fires.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`animationEventId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SoundEventId?](../../Murder/Core/Sounds/SoundEventId.html) \

#### TryPlay(SoundEventId?)

```csharp
public static ValueTask TryPlay(SoundEventId? id)
```

Plays `id` if it is not `null`; otherwise does nothing and returns a completed task. Convenience wrapper for call sites where the sound event is itself optional (e.g. an editor-configurable "sound on hit" field that may be left unset).

**Parameters** \
`id` [SoundEventId?](../../Murder/Core/Sounds/SoundEventId.html) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### UpdateListenerPosition(Vector2)

```csharp
public static void UpdateListenerPosition(Vector2 position)
```

Updates the audio listener's position (typically the camera or player position) to `position` every frame, so spatial sounds are panned/attenuated correctly relative to it.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

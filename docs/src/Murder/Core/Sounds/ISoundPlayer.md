# ISoundPlayer

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public abstract ISoundPlayer
```

Contract for the engine's audio back-end. Murder never talks to an audio middleware (e.g. FMOD) directly; every system and service that needs to play, stop, or tweak a sound goes through `Game.Sound`, which is typed as `ISoundPlayer`. This keeps the engine and gameplay code (`SoundServices`, interactions, systems) free of any dependency on a specific audio library.

**Intent:** Decouple all of the engine's audio calls from the concrete audio middleware used by a given game.

**Use-case:** A game project implements `ISoundPlayer` (backed by FMOD or any other library) and overrides `IMurderGame.CreateSoundPlayer()` to return an instance of it; `Game` stores the result and exposes it as the static `Game.Sound` property. If a game does not override `CreateSoundPlayer()`, Murder falls back to the no-op [SoundPlayer](../../../Murder/Core/Sounds/SoundPlayer.html). Gameplay code should almost never call `Game.Sound` members directly — use the higher-level, entity-aware helpers in `SoundServices` (e.g. `SoundServices.Play`, `SoundServices.Stop`, `SoundServices.SetVolume`) instead, which resolve spatial attributes and guard against edge cases (empty ids, skipped frames) before forwarding to this interface.

### ⭐ Properties

#### LastListenerPosition

```csharp
public abstract SoundSpatialAttributes LastListenerPosition { get; }
```

The most recent spatial attributes (position, facing, velocity) passed to `UpdateListener`. `SoundServices.PlayFromListenerPosition` reads this to spawn a sound that follows the listener (e.g. the camera or player) instead of a specific entity, without having to track the listener's transform itself.

**Returns** \
[SoundSpatialAttributes](../../../Murder/Core/Sounds/SoundSpatialAttributes.html) \

### ⭐ Methods

#### Initialize(string)

```csharp
public abstract void Initialize(string resourcesPath)
```

Boots the underlying audio middleware (e.g. creates the FMOD studio system) but does not load any sound banks yet. `Game` calls this once during startup with the game's binary resources directory. Implementations that don't back onto a real audio engine (like the default `SoundPlayer`) can leave this as a no-op.

**Parameters** \
`resourcesPath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
The relative path to the resource binaries.

#### LoadContentAsync(PackedSoundData)

```csharp
public abstract Task LoadContentAsync(PackedSoundData? packedData)
```

Loads the actual sound bank content asynchronously once assets are available, so the game can start showing a loading screen instead of blocking on disk/bank I/O. `packedData` describes which banks and plugins were packed for the current platform (see [PackedSoundData](../../../Murder/Data/PackedSoundData.html)); it is `null` when running from loose, unpacked assets.

**Parameters** \
`packedData` [PackedSoundData?](../../../Murder/Data/PackedSoundData.html) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### ReloadAsync()

```csharp
public abstract Task ReloadAsync()
```

Reloads every sound bank currently known to the audio middleware. Used by the editor's hot-reload flow so that audio changes made in an external tool (e.g. re-exporting an FMOD project) show up in a running game/editor session without a full restart.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### UpdateListener(SoundSpatialAttributes)

```csharp
public abstract void UpdateListener(SoundSpatialAttributes attributes)
```

Updates the position, facing, and velocity of the audio listener (typically the camera or the player). `SoundServices.UpdateListenerPosition` calls this once a frame so panning, attenuation, and Doppler effects are computed relative to the correct origin; the value passed in also becomes readable back through `LastListenerPosition`.

**Parameters** \
`attributes` [SoundSpatialAttributes](../../../Murder/Core/Sounds/SoundSpatialAttributes.html) \
Attributes of the origin of this sound.

#### UpdateEvent(SoundEventId, int, SoundSpatialAttributes)

```csharp
public abstract bool UpdateEvent(SoundEventId id, int entityId, SoundSpatialAttributes attributes)
```

Updates the spatial attributes of an already-playing event instance, so a looping sound tied to a moving entity (e.g. a footstep loop, an engine hum) keeps panning and attenuating correctly as the entity moves. `SoundServices.TrackEventSourcePosition` calls this every frame for entities that need their sound source tracked; `AmbienceTrackerSystem` and `SoundShapeTrackerSystem` use it to keep ambience/area sounds anchored to their source shape.

**Parameters** \
`id` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
Event event instance id. \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Entity id associated with this event. \
`attributes` [SoundSpatialAttributes](../../../Murder/Core/Sounds/SoundSpatialAttributes.html) \
Attributes of the origin of this sound.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
False if no event instance is found in the world, or something failed.

#### Update()

```csharp
public abstract void Update()
```

Advances the audio middleware by one frame (e.g. pumps FMOD's studio system update). `Game` calls this once per frame after the game's own update step so that queued audio commands (played events, parameter changes, bank loads) are processed and audible callbacks fire.

#### PlayEvent(SoundEventId, PlayEventInfo)

```csharp
public abstract ValueTask PlayEvent(SoundEventId id, PlayEventInfo info)
```

Plays the sound/event identified by `id`, using `info` to describe how the instance should behave: which [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) it belongs to, its [SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) flags (persistence, dedupe, exclusivity), optional [SoundSpatialAttributes](../../../Murder/Core/Sounds/SoundSpatialAttributes.html), an initial parameter value, fire-and-persist behaviour, and the entity it is tied to. This is the lowest-level entry point for starting playback; almost all gameplay code should go through `SoundServices.Play`/`SoundServices.PlayMusic`/`SoundServices.PlaySnapshot` instead, which build a correct `PlayEventInfo` for you.

**Parameters** \
`id` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
`info` [PlayEventInfo](../../../Murder/Core/Sounds/PlayEventInfo.html) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### SetParameter(SoundEventId, ParameterId, float)

```csharp
public abstract void SetParameter(SoundEventId instance, ParameterId parameter, float value)
```

Sets an instance-level audio parameter on one specific playing event, rather than every instance of that event globally. Used for adaptive audio that should only affect a single sound emitter, e.g. modulating the pitch of one specific engine loop tied to a vehicle entity.

**Parameters** \
`instance` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
`parameter` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetGlobalParameter(ParameterId, float)

```csharp
public abstract void SetGlobalParameter(ParameterId parameter, float value)
```

Sets a global audio parameter to `value`, affecting every instance of every event that reads it. Used for whole-game adaptive audio state, such as a "tension" or "combat intensity" parameter that many music/ambience events react to at once. `SetSoundParameterOnInteraction` drives this from gameplay via its `MiddlewareParameterTriggers`.

**Parameters** \
`parameter` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetGlobalParameter(ParameterId)

```csharp
public abstract float GetGlobalParameter(ParameterId parameter)
```

Reads back the current value of a global audio parameter. `SetSoundParameterOnInteraction` uses this to implement relative `Add`/`Minus` adjustments (read the current value, apply the delta, write it back) instead of only absolute `Set` operations.

**Parameters** \
`parameter` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetVolume(SoundLayer, float, float)

```csharp
public abstract void SetVolume(SoundLayer layer, float volume, float fireAfter)
```

Changes the volume of an entire [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) (e.g. `Music`, `Sfx`, `Ambience`), optionally fading over `fireAfter` seconds. `SoundServices.SetVolume` exposes both an immediate overload and one that takes a fade duration, used for things like ducking music during dialogue or fading ambience between areas.

**Parameters** \
`layer` [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \
`volume` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`fireAfter` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Resume(SoundLayer)

```csharp
public abstract bool Resume(SoundLayer layer)
```

Resumes playback of a previously paused [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html), e.g. unpausing music/ambience when leaving a pause menu.

**Parameters** \
`layer` [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Pause(SoundLayer)

```csharp
public abstract bool Pause(SoundLayer layer)
```

Pauses every currently playing sound on a [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) without stopping it, so it can later be resumed with `Resume` from the exact same playback position. Typically used to freeze `Music`/`Ambience`/`Sfx` while the game is paused.

**Parameters** \
`layer` [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsEventPlaying(SoundEventId, int)

```csharp
public abstract bool IsEventPlaying(SoundEventId id, int entityId)
```

Whether an event is being played.

**Parameters** \
`id` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
Event event instance id. \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Entity id associated with this event.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Stop(SoundLayer, bool)

```csharp
public abstract bool Stop(SoundLayer layer, bool fadeOut)
```

Stop all sounds tied to `layer`.

**Parameters** \
`layer` [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \
The target sound layer. \
`fadeOut` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether it should stop with a fade out.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether it successfully stopped.

#### Stop(SoundEventId?, int, bool)

```csharp
public abstract bool Stop(SoundEventId? id, int entityId, bool fadeOut)
```

Stop a specific sound event id. If `fadeOut` is set, this will stop with a fadeout.

**Parameters** \
`id` [SoundEventId?](../../../Murder/Core/Sounds/SoundEventId.html) \
Event event instance id. \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Entity id associated with this event. \
`fadeOut` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Apply fadeout on stop.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetVolume(SoundEventId?, float)

```csharp
public abstract void SetVolume(SoundEventId? bus, float volume)
```

Change volume.

**Parameters** \
`bus` [SoundEventId?](../../../Murder/Core/Sounds/SoundEventId.html) \
`volume` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### FetchAllBanks()

```csharp
public abstract ImmutableDictionary<string, List<string>> FetchAllBanks()
```

Fetch a list of all the banks when serializing it, separated by the supported platform. Called by the editor's asset packer (`EditorDataManager_Packer`) so it knows which sound bank files to copy into the packed build for each target platform.

**Returns** \
[ImmutableDictionary\<string, List\<string\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### FetchAllPlugins()

```csharp
public abstract ImmutableArray<string> FetchAllPlugins()
```

Fetch a list of all the plugins when serializing it. Called alongside `FetchAllBanks` by the editor's asset packer so any audio middleware plugin binaries (e.g. FMOD codec plugins) required at runtime are packed with the build.

**Returns** \
[ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

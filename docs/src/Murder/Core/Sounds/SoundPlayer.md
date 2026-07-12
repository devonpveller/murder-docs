# SoundPlayer

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public class SoundPlayer : ISoundPlayer
```

The default `ISoundPlayer` implementation used when a game does not provide its own audio back-end. Every method is a stub: it either does nothing, returns a "did nothing" value (`false`, an empty collection, a default struct), or logs an error, so the engine can run (and gameplay code can call `Game.Sound` freely) even when no real audio middleware is wired up.

**Intent:** Provide a safe, crash-free fallback sound player for projects that haven't integrated an audio library yet.

**Use-case:** `Game` uses this automatically — `IMurderGame.CreateSoundPlayer()` defaults to `new SoundPlayer()`. A game project that wants real audio (e.g. via FMOD) implements [ISoundPlayer](../../../Murder/Core/Sounds/ISoundPlayer.html) itself and overrides `CreateSoundPlayer()` to return that implementation instead. If `PlayEvent` is ever reached on this default player, it logs an error via `GameLogger`, since that indicates the game forgot to supply a real sound player.

**Implements:** _[ISoundPlayer](../../../Murder/Core/Sounds/ISoundPlayer.html)_

### ⭐ Constructors

```csharp
public SoundPlayer()
```

Default constructor; the type has no state, so there is nothing to initialize.

### ⭐ Properties

#### LastListenerPosition

```csharp
public virtual SoundSpatialAttributes LastListenerPosition { get; }
```

Always returns a default (all-zero) `SoundSpatialAttributes`, since this stub never tracks a listener.

**Returns** \
[SoundSpatialAttributes](../../../Murder/Core/Sounds/SoundSpatialAttributes.html) \

### ⭐ Methods

#### Initialize(string)

```csharp
public virtual void Initialize(string resourcesPath)
```

No-op: there is no audio middleware to initialize.

**Parameters** \
`resourcesPath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### LoadContentAsync(PackedSoundData)

```csharp
public virtual Task LoadContentAsync(PackedSoundData? packedData)
```

No-op: returns `Task.CompletedTask` immediately without loading any bank data.

**Parameters** \
`packedData` [PackedSoundData?](../../../Murder/Data/PackedSoundData.html) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### ReloadAsync()

```csharp
public virtual Task ReloadAsync()
```

No-op: returns `Task.CompletedTask` immediately.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### UpdateListener(SoundSpatialAttributes)

```csharp
public virtual void UpdateListener(SoundSpatialAttributes attributes)
```

No-op: the passed-in listener attributes are discarded.

**Parameters** \
`attributes` [SoundSpatialAttributes](../../../Murder/Core/Sounds/SoundSpatialAttributes.html) \

#### Update()

```csharp
public virtual void Update()
```

No-op: there is no middleware to advance each frame.

#### PlayEvent(SoundEventId, PlayEventInfo)

```csharp
public virtual ValueTask PlayEvent(SoundEventId _, PlayEventInfo properties)
```

Logs an error via `GameLogger` stating that the default sound player has been deprecated/should not be reached, then returns a completed `ValueTask` without playing anything. Reaching this method means the game never registered a real `ISoundPlayer` via `IMurderGame.CreateSoundPlayer()`.

**Parameters** \
`_` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
`properties` [PlayEventInfo](../../../Murder/Core/Sounds/PlayEventInfo.html) \

**Returns** \
[ValueTask](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask?view=net-7.0) \

#### UpdateEvent(SoundEventId, int, SoundSpatialAttributes)

```csharp
public virtual bool UpdateEvent(SoundEventId id, int entityId, SoundSpatialAttributes attributes)
```

Always returns `false`: there is no live event instance to update.

**Parameters** \
`id` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`attributes` [SoundSpatialAttributes](../../../Murder/Core/Sounds/SoundSpatialAttributes.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetVolume(SoundEventId?, float)

```csharp
public virtual void SetVolume(SoundEventId? _, float volume)
```

Change volume. No-op in this default implementation.

**Parameters** \
`_` [SoundEventId?](../../../Murder/Core/Sounds/SoundEventId.html) \
`volume` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Stop(SoundEventId?, int, bool)

```csharp
public virtual bool Stop(SoundEventId? _, int __, bool ___)
```

Always returns `false`: there is nothing playing to stop.

**Parameters** \
`_` [SoundEventId?](../../../Murder/Core/Sounds/SoundEventId.html) \
`__` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`___` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Stop(SoundLayer, bool)

```csharp
public virtual bool Stop(SoundLayer layer, bool fadeOut)
```

Always returns `false`: there is nothing playing on any layer to stop.

**Parameters** \
`layer` [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \
`fadeOut` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Resume(SoundLayer)

```csharp
public virtual bool Resume(SoundLayer layer)
```

Always returns `false`: there is nothing paused to resume.

**Parameters** \
`layer` [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Pause(SoundLayer)

```csharp
public virtual bool Pause(SoundLayer layer)
```

Always returns `false`: there is nothing playing to pause.

**Parameters** \
`layer` [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetParameter(SoundEventId, ParameterId, float)

```csharp
public virtual void SetParameter(SoundEventId instance, ParameterId parameter, float value)
```

No-op: there is no live event instance to set a parameter on.

**Parameters** \
`instance` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
`parameter` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetGlobalParameter(ParameterId, float)

```csharp
public virtual void SetGlobalParameter(ParameterId parameter, float value)
```

No-op: there is no middleware state to write the parameter into.

**Parameters** \
`parameter` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetGlobalParameter(ParameterId)

```csharp
public virtual float GetGlobalParameter(ParameterId _)
```

Always returns `0`.

**Parameters** \
`_` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### FetchAllBanks()

```csharp
public virtual ImmutableDictionary<string, List<string>> FetchAllBanks()
```

Always returns an empty dictionary: this stub has no banks to report.

**Returns** \
[ImmutableDictionary\<string, List\<string\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### FetchAllPlugins()

```csharp
public virtual ImmutableArray<string> FetchAllPlugins()
```

Always returns an empty array: this stub has no plugins to report.

**Returns** \
[ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### IsEventPlaying(SoundEventId, int)

```csharp
public virtual bool IsEventPlaying(SoundEventId id, int entityId)
```

Always returns `false`: nothing is ever playing in this stub.

**Parameters** \
`id` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetVolume(SoundLayer, float, float)

```csharp
public virtual void SetVolume(SoundLayer _, float __, float ___)
```

No-op: there is no layer volume state to change.

**Parameters** \
`_` [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \
`__` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`___` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

# FireAndPersistInfo

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct FireAndPersistInfo
```

Describes a sound instance that should be started and then left to play on its own for a fixed duration (rather than being explicitly stopped by gameplay code). Declared inside `ISoundPlayer.cs` alongside `PlayEventInfo`, whose `FireAndPersist` property carries this value.

**Intent:** Give a "fire and forget" playback a self-contained lifetime and, optionally, the ability to keep tracking the audio listener while it plays.

**Use-case:** `SoundServices.PlayFromListenerPosition(SoundEventId, float duration)` builds a `FireAndPersistInfo` when `duration` is non-zero, setting `PlayingSoundFlags.FollowListenerPosition` so the one-shot sound trails the listener for its whole lifetime instead of being explicitly tracked frame-by-frame by gameplay code.

### ⭐ Constructors

```csharp
public FireAndPersistInfo()
```

Creates a `FireAndPersistInfo` with no duration (`0`) and no flags.

```csharp
public FireAndPersistInfo(float duration, PlayingSoundFlags flags)
```

Creates a `FireAndPersistInfo` with an explicit duration and behaviour flags.

**Parameters** \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
How long, in seconds, the instance should keep playing. \
`flags` [PlayingSoundFlags](../../../Murder/Core/Sounds/PlayingSoundFlags.html) \
Additional playback behaviour flags.

### ⭐ Properties

#### Duration

```csharp
public float Duration { get; init; }
```

How long, in seconds, the instance should keep playing before it is implicitly stopped. A value of `0` means no automatic duration is applied.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Flags

```csharp
public PlayingSoundFlags Flags { get; init; }
```

Additional playback behaviour flags, e.g. whether the instance should follow the listener's position for its whole lifetime. See `PlayingSoundFlags`.

**Returns** \
[PlayingSoundFlags](../../../Murder/Core/Sounds/PlayingSoundFlags.html) \

⚡

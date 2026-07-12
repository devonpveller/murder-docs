# SoundProperties

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
[Flags]
public enum SoundProperties
```

Flags that control how a newly played sound event instance behaves and interacts with other sounds. Declared inside `ISoundPlayer.cs` alongside `PlayEventInfo`, whose `Properties` field carries this value into `ISoundPlayer.PlayEvent`.

**Intent:** Fine-tune how a sound event is managed by the sound system without adding extra parameters to every play call.

**Use-case:** Pass `SoundProperties` flags to `SoundServices.Play`/`PlayWithParameter` (or set `PlayEventInfo.Properties` directly). Combine flags with the bitwise OR operator, e.g. `SoundProperties.Persist | SoundProperties.SkipIfAlreadyPlaying`. `SoundServices.Play` automatically adds `Persist` whenever the target [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) is `Music` or `Snapshot`, since those layers are expected to keep playing across scene transitions.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### None

```csharp
public static const SoundProperties None;
```

No special playback flags; the event plays and behaves with default rules (not persisted, always started even if already playing, does not stop anything else).

**Returns** \
[SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \

#### Persist

```csharp
public static const SoundProperties Persist;
```

Marks the event instance so its [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) is persisted, i.e. it should keep playing across scene/world transitions instead of being torn down with the current scene. Required for music and ambience that must continue seamlessly when the player moves between scenes; `SoundServices.PlayMusic` and `PlaySnapshot` always set this flag.

**Returns** \
[SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \

#### SkipIfAlreadyPlaying

```csharp
public static const SoundProperties SkipIfAlreadyPlaying;
```

Does not start a new instance if the same event is already playing, preventing duplicate/overlapping instances of the same sound from stacking up (e.g. re-triggering a looping ambience trigger volume repeatedly).

**Returns** \
[SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \

#### StopOtherEventsInLayer

```csharp
public static const SoundProperties StopOtherEventsInLayer;
```

Stops every other event currently playing on the same [SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) before starting this one, making the new event exclusive within its layer. Useful for one-shot music/snapshot changes where only one track should ever be audible on that layer at a time.

**Returns** \
[SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \

⚡

# SoundLayer

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed enum SoundLayer : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Groups sound events into broad categories so playback, volume, pausing, and stopping can be controlled per-category instead of per-event.

**Intent:** Let engine and gameplay code target a whole category of sounds at once (e.g. duck all `Sfx`, pause everything while paused, fade `Music` between areas) instead of tracking every individual playing instance.

**Use-case:** Pass a `SoundLayer` to `ISoundPlayer`/`SoundServices` methods such as `SetVolume`, `Stop`, `Pause`, and `Resume`. `SoundServices.Play` automatically adds `SoundProperties.Persist` whenever the target layer is `Music` or `Snapshot`, since those are expected to survive scene transitions; `AmbienceTrackerSystem` and related systems key ambience sounds to the `Ambience` layer so they can be stopped or faded as a group when leaving an area.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Ambience

```csharp
public static const SoundLayer Ambience;
```

Looping environmental/background sounds (e.g. wind, room tone) tied to areas or trigger volumes.

**Returns** \
[SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

#### Any

```csharp
public static const SoundLayer Any;
```

Wildcard layer matching every sound regardless of its actual layer. Used e.g. by `SoundServices.StopAll` to stop everything at once, and as the default layer for `SoundServices.Play` overloads that don't specify one.

**Returns** \
[SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

#### Music

```csharp
public static const SoundLayer Music;
```

Music tracks. `SoundServices.Play`/`PlayMusic` automatically mark events on this layer as `SoundProperties.Persist` so they survive scene transitions.

**Returns** \
[SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

#### Sfx

```csharp
public static const SoundLayer Sfx;
```

One-shot and looping sound effects (e.g. footsteps, impacts, UI feedback).

**Returns** \
[SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

#### Snapshot

```csharp
public static const SoundLayer Snapshot;
```

FMOD snapshots, i.e. mix state changes rather than audible sound sources on their own. Like `Music`, `SoundServices.Play`/`PlaySnapshot` automatically mark these as `SoundProperties.Persist`.

**Returns** \
[SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

⚡

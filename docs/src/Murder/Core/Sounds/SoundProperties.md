# SoundProperties

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed enum SoundProperties : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags that control the playback behaviour of a sound event instance.

**Intent:** Fine-tune how a sound event is managed by the sound system.

**Use-case:** Pass `SoundProperties` flags to `SoundServices.Play()`. Combine flags with the bitwise OR operator, e.g. `SoundProperties.Persist | SoundProperties.SkipIfAlreadyPlaying`.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### None
```csharp
public static const SoundProperties None;
```

No special playback flags.

**Returns** \
[SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \
#### Persist
```csharp
public static const SoundProperties Persist;
```

Keeps the event instance alive across scene transitions. Required for music that should continue playing.

**Returns** \
[SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \
#### SkipIfAlreadyPlaying
```csharp
public static const SoundProperties SkipIfAlreadyPlaying;
```

Does not start a new instance if the same event is already playing.

**Returns** \
[SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \
#### StopOtherMusic
```csharp
public static const SoundProperties StopOtherMusic;
```

Stops all other events on the same sound layer before starting this one.

**Returns** \
[SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \


⚡
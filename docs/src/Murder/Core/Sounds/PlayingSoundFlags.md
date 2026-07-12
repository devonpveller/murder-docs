# PlayingSoundFlags

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
[Flags]
public sealed enum PlayingSoundFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags describing how a "fire and persist" sound instance should keep playing after it starts. Declared inside `ISoundPlayer.cs` alongside `FireAndPersistInfo`, whose `Flags` property carries this value.

**Intent:** Let a sound instance track a moving origin (the listener) without being explicitly re-anchored every frame by gameplay code.

**Use-case:** Set `FireAndPersistInfo.Flags` to `PlayingSoundFlags.FollowListenerPosition` when building a `PlayEventInfo.FireAndPersist` value so the sound keeps following the audio listener (e.g. the camera or player) for its whole lifetime instead of staying fixed at the position it was played from. `SoundServices.PlayFromListenerPosition` uses this to spawn one-shot sounds that should trail the listener.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### FollowListenerPosition

```csharp
public static const PlayingSoundFlags FollowListenerPosition;
```

Keeps the sound instance anchored to the audio listener's position as it moves, instead of the fixed position it was played from. Only valid if `PlayEventInfo.EntityId` is `-1` (i.e. the sound isn't already tied to a specific entity).

**Returns** \
[PlayingSoundFlags](../../../Murder/Core/Sounds/PlayingSoundFlags.html) \

#### None

```csharp
public static const PlayingSoundFlags None;
```

No special behaviour; the sound instance stays at the position it was played from.

**Returns** \
[PlayingSoundFlags](../../../Murder/Core/Sounds/PlayingSoundFlags.html) \

⚡

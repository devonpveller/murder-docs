# PlayEventInfo

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct PlayEventInfo
```

All the information needed to start a sound event instance. Declared inside `ISoundPlayer.cs` and passed to `ISoundPlayer.PlayEvent(SoundEventId, PlayEventInfo)`.

**Intent:** Bundle every optional piece of playback context (layer, flags, spatial data, initial parameter, fire-and-persist behaviour, owning entity) into a single value instead of a long parameter list, so `ISoundPlayer.PlayEvent` has one stable signature no matter how playback should behave.

**Use-case:** Built by the `SoundServices` helpers (`Play`, `PlayMusic`, `PlaySnapshot`, `PlayFromListenerPosition`, `PlayWithParameter`) rather than constructed by hand in most gameplay code — those methods resolve an entity's spatial attributes, decide whether `SoundProperties.Persist` should be added for `Music`/`Snapshot` layers, and build the correct `PlayEventInfo` before calling `Game.Sound.PlayEvent`.

### ⭐ Constructors

```csharp
public PlayEventInfo()
```

Creates a `PlayEventInfo` with all default values: no persistence/dedupe/exclusivity flags, the `Any` layer, no spatial attributes, no initial parameter, no fire-and-persist behaviour, and not tied to any entity (`EntityId` is `-1`).

### ⭐ Properties

#### Attributes

```csharp
public SoundSpatialAttributes? Attributes { get; init; }
```

Optional spatial data (position, facing, velocity) for this instance. Left `null` for non-spatial (e.g. UI or global) sounds.

**Returns** \
[SoundSpatialAttributes?](../../../Murder/Core/Sounds/SoundSpatialAttributes.html) \

#### EntityId

```csharp
public int EntityId { get; init; }
```

Entity id that is tied to this event.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### FireAndPersist

```csharp
public FireAndPersistInfo? FireAndPersist { get; init; }
```

Optional fire-and-forget playback behaviour (e.g. auto-stop after a duration, following the listener). See `FireAndPersistInfo`.

**Returns** \
[FireAndPersistInfo?](../../../Murder/Core/Sounds/FireAndPersistInfo.html) \

#### Layer

```csharp
public SoundLayer Layer { get; init; }
```

Event layer, only persisted if `Properties` has `SoundProperties.Persist` set.

**Returns** \
[SoundLayer](../../../Murder/Core/Sounds/SoundLayer.html) \

#### Parameter

```csharp
public ParameterValue? Parameter { get; init; }
```

Optional initial value for an instance-level parameter to set as soon as the event starts.

**Returns** \
[ParameterValue?](../../../Murder/Core/Sounds/ParameterValue.html) \

#### Properties

```csharp
public SoundProperties Properties { get; init; }
```

Flags controlling persistence, deduplication, and exclusivity for this instance. See `SoundProperties`.

**Returns** \
[SoundProperties](../../../Murder/Core/Sounds/SoundProperties.html) \

⚡

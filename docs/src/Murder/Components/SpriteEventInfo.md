# SpriteEventInfo

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteEventInfo
```

Describes a single animation-frame event binding: the frame marker `Id` it fires on, an optional sound to play, whether that sound should persist as a layer, and an optional list of interactions to run.

**Intent:** Give the editor an ordered, human-editable array shape for animation events, which `WorldHelper.ToEventListener` then converts into the dictionary form (`Id` → `SpriteEventInfo`) that `EventListenerComponent` uses at runtime for O(1) lookup by frame marker name.

**Use-case:** Populate `EventListenerEditorComponent.Events` with one `SpriteEventInfo` per named frame marker defined in an Aseprite file (e.g. a "footstep" or "hit" tag); `EventListenerSystem`/`WorldHelper.ToEventListener` reads `Id`, `Sound`, `Persisted`, and `Interactions` to fire the right sound and interactions whenever the sprite's animation reaches that frame. Use `WithPersist` to mark the bound sound as a persisted layer (e.g. an ambience loop) rather than a one-shot effect.

### ⭐ Constructors

```csharp
public SpriteEventInfo(string id)
```

Creates an event bound to `id` with no sound and no interactions — useful for markers that should only trigger interactions, or as a placeholder while authoring.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

```csharp
public SpriteEventInfo(string id, SoundEventId sound)
```

Creates an event that plays `sound` when frame marker `id` is reached, with no persistence layer and no interactions.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`sound` [SoundEventId](../../Murder/Core/Sounds/SoundEventId.html) \

```csharp
public SpriteEventInfo(string id, SoundEventId? sound, SoundLayer? persisted, ImmutableArray<T>? interactions)
```

Full constructor that sets every field explicitly.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`sound` [SoundEventId?](../../Murder/Core/Sounds/SoundEventId.html) \
`persisted` [SoundLayer?](../../Murder/Core/Sounds/SoundLayer.html) \
`interactions` [ImmutableArray\<T\>?](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties

#### Id

```csharp
public readonly string Id;
```

Name of the animation frame marker (as defined in the Aseprite file) that triggers this event. Marked `[Tooltip("Id listed in sprite")]` in the editor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Interactions

```csharp
public readonly ImmutableArray<T>? Interactions { get; init; }
```

Optional list of `IInteractiveComponent` instances to run when this frame marker is reached, in addition to (or instead of) playing `Sound`. Defaults to `null` (no interactions).

**Returns** \
[ImmutableArray\<T\>?](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Persisted

```csharp
public readonly SoundLayer? Persisted;
```

When set, the sound triggered by this event is played on the given persisted `SoundLayer` (e.g. an ambience/looping layer) instead of as a one-shot effect. `null` means the sound is a plain one-shot.

**Returns** \
[SoundLayer?](../../Murder/Core/Sounds/SoundLayer.html) \

#### Sound

```csharp
public readonly SoundEventId? Sound;
```

Optional sound event played when this frame marker is reached. `null` means no sound is triggered by this event.

**Returns** \
[SoundEventId?](../../Murder/Core/Sounds/SoundEventId.html) \

### ⭐ Methods

#### WithPersist(SoundLayer)

```csharp
public SpriteEventInfo WithPersist(SoundLayer persisted)
```

Returns a copy of this event info with `Persisted` set to the given `SoundLayer`, so its sound is treated as a persisted layer rather than a one-shot effect.

**Parameters** \
`persisted` [SoundLayer](../../Murder/Core/Sounds/SoundLayer.html) \

**Returns** \
[SpriteEventInfo](../../Murder/Components/SpriteEventInfo.html) \

⚡

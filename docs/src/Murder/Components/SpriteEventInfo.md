# SpriteEventInfo

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteEventInfo
```

Describes an event that fires on a specific frame of a sprite animation, optionally triggering a sound effect and/or a list of interactions.

**Intent:** Map a named animation frame marker to a sound event and/or gameplay interactions.

**Use-case:** Add one `SpriteEventInfo` per named frame marker in an Aseprite file to an `EventListenerEditorComponent`; the system fires sounds and interactions automatically when that frame is reached during playback.

### ⭐ Constructors
```csharp
public SpriteEventInfo(string id, T? sound, bool persist)
```

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`sound` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`persist` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public SpriteEventInfo(string id, T? sound)
```

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`sound` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

```csharp
public SpriteEventInfo(string id)
```

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Id
```csharp
public readonly string Id;
```

Name of the animation frame marker (as defined in the Aseprite file) that triggers this event.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Persist
```csharp
public readonly bool Persist;
```

When true, the triggered sound is treated as a persistent (looping/ambience) layer rather than a one-shot effect.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Sound
```csharp
public readonly T? Sound;
```

Optional sound event played when this frame marker is reached.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
### ⭐ Methods
#### WithPersist(bool)
```csharp
public SpriteEventInfo WithPersist(bool persist)
```

Returns a copy of this event info with the `Persist` flag updated.

**Parameters** \
`persist` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[SpriteEventInfo](../../Murder/Components/SpriteEventInfo.html) \



⚡
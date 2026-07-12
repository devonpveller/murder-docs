# EventListenerComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct EventListenerComponent : IComponent
```

Maps animation event IDs to `SpriteEventInfo` descriptors that specify what sounds and interactions fire when the animation reaches that event frame.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Wires animation frame events (authored in Aseprite tags) to runtime actions such as sound playback or interaction chains, in the efficient dictionary form used at runtime (as opposed to the array form authored in the editor).

**Use-case:** Not usually constructed by hand — `EntityBuilder` and `WorldHelper.ToEventListener` convert an [EventListenerEditorComponent](../../Murder/Components/EventListenerEditorComponent.html) (authored in the editor) into this component when a prefab is instantiated. `EventListenerSystem` listens for `AnimationEventMessage`, looks up the fired event id in `Events`, and (unless the entity also has `MuteEventsComponent`) plays the mapped sound and/or triggers the mapped interactions; `EventPersistedOnEntityListenerSystem` stops any persisted sounds from this map when the entity's `PlayingPersistedEventComponent` is removed.

### ⭐ Constructors

```csharp
public EventListenerComponent()
```

```csharp
public EventListenerComponent(ImmutableDictionary<TKey, TValue> events)
```

Creates a component with the given event-to-info mapping.

**Parameters** \
`events` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

### ⭐ Properties

#### Events

```csharp
public readonly ImmutableDictionary<TKey, TValue> Events;
```

Map of animation event ID string to its `SpriteEventInfo` (sound and interactions).

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

### ⭐ Methods

#### Merge(ImmutableDictionary<TKey, TValue>)

```csharp
public EventListenerComponent Merge(ImmutableDictionary<TKey, TValue> events)
```

Returns a new component with the given `events` merged into the existing map, overwriting any duplicate keys.

**Parameters** \
`events` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

**Returns** \
[EventListenerComponent](../../Murder/Components/EventListenerComponent.html) \

⚡

# EventListenerComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct EventListenerComponent : IComponent
```

Maps animation event IDs to `SpriteEventInfo` descriptors that specify what sounds and interactions fire when the animation reaches that event frame.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Wires animation frame events (authored in Aseprite tags) to runtime actions such as sound playback or interaction chains.

**Use-case:** Added automatically from `EventListenerEditorComponent` when the world loads; `EventListenerSystem` reads `Events` each frame and executes the mapped sounds and interactions.

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
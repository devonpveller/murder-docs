# WorldHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class WorldHelper
```

Conversion helpers that translate editor-authored, array-based component representations into the dictionary-based runtime shape systems actually consume.

**Intent:** Provides the translation layer between editor-only component representations and their optimized runtime counterparts. Currently only covers animation event listeners.

**Use-case:** Call `ToEventListener` when building a scene to convert `EventListenerEditorComponent` (with an ordered array of events) into the runtime `EventListenerComponent` (with a fast case-insensitive dictionary), so `EventListenerSystem` doesn't need to linearly scan an array on every lookup.

### ⭐ Methods

#### ToEventListener(EventListenerEditorComponent)

```csharp
public EventListenerComponent ToEventListener(EventListenerEditorComponent c)
```

Converts an editor event-listener component (with an ordered array of events) to a runtime `EventListenerComponent` backed by a fast case-insensitive dictionary. Delegates to `ToEventListener(ImmutableArray<SpriteEventInfo>)`.

**Parameters** \
`c` [EventListenerEditorComponent](../../Murder/Components/EventListenerEditorComponent.html) \

**Returns** \
[EventListenerComponent](../../Murder/Components/EventListenerComponent.html) \

#### ToEventListener(ImmutableArray\<SpriteEventInfo\>)

```csharp
public ImmutableDictionary<string, SpriteEventInfo> ToEventListener(ImmutableArray<SpriteEventInfo> messages)
```

Builds the id-to-`SpriteEventInfo` dictionary used by `ToEventListener(EventListenerEditorComponent)` from a raw array of events, skipping any entry with a `null` `SpriteEventInfo.Id`. If multiple entries share the same id (case-insensitively), the last one wins.

**Parameters** \
`messages` [ImmutableArray\<SpriteEventInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[ImmutableDictionary\<string, SpriteEventInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

⚡

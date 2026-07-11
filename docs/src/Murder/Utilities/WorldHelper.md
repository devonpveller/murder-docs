# WorldHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class WorldHelper
```

Conversion helpers for transforming editor-side world data into runtime-ready components.

**Intent:** Provides the translation layer between editor-only component representations and their optimized runtime counterparts.

**Use-case:** Call `ToEventListener` when building a scene to convert `EventListenerEditorComponent` (with an array of events) into the runtime `EventListenerComponent` (with a fast dictionary).

### ⭐ Methods
#### ToEventListener(EventListenerEditorComponent)
```csharp
public EventListenerComponent ToEventListener(EventListenerEditorComponent c)
```

Converts an editor event-listener component (with an array of events) to a runtime `EventListenerComponent` backed by a fast case-insensitive dictionary.

**Parameters** \
`c` [EventListenerEditorComponent](../../Murder/Components/EventListenerEditorComponent.html) \

**Returns** \
[EventListenerComponent](../../Murder/Components/EventListenerComponent.html) \



⚡
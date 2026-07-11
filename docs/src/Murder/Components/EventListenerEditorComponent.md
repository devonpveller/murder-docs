# EventListenerEditorComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct EventListenerEditorComponent : IComponent
```

Editor-facing component that stores a list of `SpriteEventInfo` entries authored in the inspector, later converted to a runtime `EventListenerComponent`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a serializable, editor-editable format for animation event bindings that is converted to the efficient runtime dictionary form on world load.

**Use-case:** Set up animation event → sound/interaction bindings in the editor via this component; `WorldHelper.ToEventListener` converts it to `EventListenerComponent` at runtime.

### ⭐ Constructors
```csharp
public EventListenerEditorComponent()
```

### ⭐ Properties
#### Events
```csharp
public readonly ImmutableArray<T> Events;
```

Ordered list of `SpriteEventInfo` entries defining the animation events and their associated sounds and interactions.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
# EventListenerEditorComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct EventListenerEditorComponent : IComponent
```

Editor-facing component that stores a list of [SpriteEventInfo](../../Murder/Components/SpriteEventInfo.html) entries authored in the inspector, later converted to a runtime [EventListenerComponent](../../Murder/Components/EventListenerComponent.html).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a serializable, editor-editable, ordered array format for animation event bindings — as opposed to the dictionary form `EventListenerComponent` uses at runtime — because it is friendlier to author, diff, and display in the inspector (via the `EventListenerEditor` custom component drawer). It carries the `[SoundPlayer]` attribute so the editor's sound-preview tooling recognizes it.

**Use-case:** Author animation event → sound/interaction bindings in the editor via this component (added to an entity, or embedded directly as in `EditorCosmeticsAsset.Sounds` and `SpeakerAsset.Events`). `WorldHelper.ToEventListener` (called from `EntityBuilder` and `Stage_Instances`) converts an instance to a runtime `EventListenerComponent` when an entity/prefab is instantiated into the world.

### ⭐ Constructors

```csharp
public EventListenerEditorComponent()
```

Creates the component with an empty `Events` array.

```csharp
public EventListenerEditorComponent(ImmutableArray<T> events)
```

Creates the component with an explicit ordered list of `SpriteEventInfo` bindings.

**Parameters** \
`events` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties

#### Events

```csharp
public readonly ImmutableArray<T> Events { get; init; }
```

Ordered list of `SpriteEventInfo` entries defining the animation events and their associated sounds and interactions.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

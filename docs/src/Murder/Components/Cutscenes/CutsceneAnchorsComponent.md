# CutsceneAnchorsComponent

**Namespace:** Murder.Components.Cutscenes \
**Assembly:** Murder.dll

```csharp
public sealed struct CutsceneAnchorsComponent : IComponent
```

Runtime lookup table of named anchor points for a cutscene entity, keyed by anchor name.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** This is the runtime-friendly form of a cutscene's anchors. While [CutsceneAnchorsEditorComponent](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html) (backed by an ordered list of [AnchorId](../../../Murder/Components/Serialization/AnchorId.html)) is the authoring-time representation edited in the level/cutscene editor, `WorldProcessor` converts it into this dictionary-backed component when the world loads — trading the editable ordered list for constant-time name lookups — and removes the editor component from the entity in the process.

**Use-case:** Read `Anchors` from cutscene playback code (camera moves, "move entity to anchor" actions, dialogue staging, etc.) to resolve a named anchor to its world-space [Anchor](../../../Murder/Core/Cutscenes/Anchor.html). This component is marked `[RuntimeOnly]` because it is derived data rebuilt from the editor component, and `[PersistOnSave]` so that any cutscene state referencing these anchors survives a save/reload while a cutscene is mid-playback.

### ⭐ Constructors

```csharp
public CutsceneAnchorsComponent()
```

Default constructor; `Anchors` starts as an empty dictionary.

```csharp
public CutsceneAnchorsComponent(ImmutableDictionary<TKey, TValue> anchors)
```

Creates the component pre-populated with the given name-to-anchor lookup table.

**Parameters** \
`anchors` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) — map of anchor name to world-space position. \

### ⭐ Properties

#### Anchors

```csharp
public readonly ImmutableDictionary<TKey, TValue> Anchors;
```

Maps each anchor's name to its world-space [Anchor](../../../Murder/Core/Cutscenes/Anchor.html) position, used to resolve named anchors during cutscene playback.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

⚡

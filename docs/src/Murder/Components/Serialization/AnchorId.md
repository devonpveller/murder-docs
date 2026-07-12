# AnchorId

**Namespace:** Murder.Components.Serialization \
**Assembly:** Murder.dll

```csharp
public sealed struct AnchorId
```

Pairs a designer-facing string name with an [Anchor](../../../Murder/Core/Cutscenes/Anchor.html) world-space position.

**Intent:** This is the authoring-time (editable, ordered-list) representation of a single named cutscene anchor: one entry of [CutsceneAnchorsEditorComponent.Anchors](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html). At world-load time, `WorldProcessor` walks that list and converts each `AnchorId` into a name-to-[Anchor](../../../Murder/Core/Cutscenes/Anchor.html) dictionary entry on the runtime [CutsceneAnchorsComponent](../../../Murder/Components/Cutscenes/CutsceneAnchorsComponent.html).

**Use-case:** Add one `AnchorId` per named location a cutscene needs to address (camera targets, character marks, etc.) to the `Anchors` list on a [CutsceneAnchorsEditorComponent](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html) — normally through the cutscene editor's anchor tools rather than by hand.

### ⭐ Constructors

```csharp
public AnchorId()
```

Default constructor; `Id` is an empty string and `Anchor` is a default anchor.

```csharp
public AnchorId(string id, Anchor anchor)
```

Creates a named anchor pairing `id` with its world-space `anchor`.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — unique name for this anchor. \
`anchor` [Anchor](../../../Murder/Core/Cutscenes/Anchor.html) — world-space position/data for this anchor. \

### ⭐ Properties

#### Anchor

```csharp
public readonly Anchor Anchor;
```

The world-space anchor (position, and any additional anchor data) associated with [Id](#id).

**Returns** \
[Anchor](../../../Murder/Core/Cutscenes/Anchor.html) \

#### Id

```csharp
public readonly string Id;
```

Unique, human-readable name used to reference this anchor from cutscene scripts and from the cutscene editor. `CutsceneAnchorsEditorComponent`'s edit helpers (`WithAnchorAt`, `WithoutAnchorAt`) match this name case-insensitively; `FindAnchor` matches it case-sensitively.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

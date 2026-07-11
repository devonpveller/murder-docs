# AnchorId

**Namespace:** Murder.Components.Serialization \
**Assembly:** Murder.dll

```csharp
public sealed struct AnchorId
```

Pairs a string identifier with an [Anchor](../../../Murder/Core/Cutscenes/Anchor.html) position, used to mark named points within a cutscene.

**Intent:** Associate a human-readable name with a world-space anchor point so cutscene scripts can reference positions by name.

**Use-case:** Add to the `Anchors` list on a [CutsceneAnchorsEditorComponent](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html) for every named location a cutscene needs to address (e.g. camera targets, character marks).

### ⭐ Constructors
```csharp
public AnchorId()
```

```csharp
public AnchorId(string id, Anchor anchor)
```

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`anchor` [Anchor](../../../Murder/Core/Cutscenes/Anchor.html) \

### ⭐ Properties
#### Anchor
```csharp
public readonly Anchor Anchor;
```

The world-space anchor position associated with this identifier.

**Returns** \
[Anchor](../../../Murder/Core/Cutscenes/Anchor.html) \
#### Id
```csharp
public readonly string Id;
```

Unique name used by cutscene scripts to reference this anchor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡
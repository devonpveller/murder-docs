# DialogueLineInfo

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct DialogueLineInfo
```

Pairs a `DialogueId` with its `LineInfo` override; this is the flat, serializable list element backing a character asset's internal storage, which is expanded into a lookup dictionary keyed by `DialogueId` at runtime.

**Intent:** Provides a serializable (list-friendly) representation of the `DialogueId` → `LineInfo` mapping, since immutable dictionaries themselves are not directly serialized by the engine's asset format.

**Use-case:** `CharacterAsset` stores its per-line overrides as an `ImmutableArray<DialogueLineInfo>` and lazily rebuilds an `ImmutableDictionary<DialogueId, LineInfo>` from it on first access; editor code that edits overrides mutates this list indirectly through `CharacterAsset` methods such as `SetCustomPortraitAt` and `SetActionAt`.

### ⭐ Constructors

```csharp
public DialogueLineInfo()
```

Creates an empty entry with a default `DialogueId` and an empty `LineInfo`.

```csharp
public DialogueLineInfo(DialogueId id)
```

Creates an entry for `id` with a default (empty) `LineInfo`.

**Parameters** \
`id` [DialogueId](../../../Murder/Core/Dialogs/DialogueId.html) \

### ⭐ Properties

#### Id

```csharp
public readonly DialogueId Id;
```

The dialogue item this override data applies to.

**Returns** \
[DialogueId](../../../Murder/Core/Dialogs/DialogueId.html) \

#### Info

```csharp
public LineInfo Info { get; init; }
```

The override data itself.

**Returns** \
[LineInfo](../../../Murder/Core/Dialogs/LineInfo.html) \

⚡

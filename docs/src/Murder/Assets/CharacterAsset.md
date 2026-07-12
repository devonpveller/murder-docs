# CharacterAsset

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class CharacterAsset : GameAsset
```

Defines the dialogue tree(s) for a single speaking character: a named set of `Situation` dialogue branches, plus per-line overrides (custom speaker/portrait, ECS component, event name, or action) that the editor's dialogue tools let a writer attach to individual dialogue lines.

**Intent:** Bundle everything a character's dialogue needs into one editor-authored asset -- who is speaking (`Owner`, `Portrait`), what they can say (`Situations`), and any line-specific gameplay hooks (`Data`) -- so the dialogue runtime can drive a full conversation from a single GUID reference.

**Use-case:** Create one `CharacterAsset` per speaking character (NPC, narrator, etc.) and author its `Situation`s in the dialogue editor. Reference the asset's `Guid` from whatever triggers dialogue (e.g. an NPC's interaction data), then use `CharacterRuntime` to walk the graph at runtime, calling `TryFetchSituation` to start a specific branch by name. Use `SetCustomPortraitAt`/`SetCustomComponentAt`/`SetActionAt`/`SetEventInfoAt` (usually via the editor UI) to attach per-line overrides, and `PrunUnusedData`/`PrunUnusedComponents` to keep that override data tidy as the script changes.

**Implements:** _[GameAsset](../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors

```csharp
public CharacterAsset()
```

### ⭐ Properties

#### CanBeCreated

```csharp
public virtual bool CanBeCreated { get; }
```

Determines if the asset can be created, override to change this capability. `CharacterAsset` uses the inherited default (`true`), so writers can create new characters from the editor's asset browser.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeDeleted

```csharp
public virtual bool CanBeDeleted { get; }
```

Determines if the asset can be deleted, override to change this capability. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeRenamed

```csharp
public virtual bool CanBeRenamed { get; }
```

Determines if the asset can be renamed, override to change this capability. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeSaved

```csharp
public virtual bool CanBeSaved { get; }
```

Determines if the asset can be saved, override to change this capability. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Data

```csharp
public ImmutableDictionary<TKey, TValue> Data { get; }
```

Per-line override data (custom speaker/portrait, ECS component, event name, action, flags), keyed by the stable `DialogueId` of the dialogue line or action it applies to (maps `DialogueId` to `LineInfo`). Lazily built from the serialized data and cached until `OnModified` clears the cache. The dialogue runtime consults this to know whether a specific line should use a different portrait, trigger a component, or fire an event/action when it plays.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### EditorColor

```csharp
public virtual Vector4 EditorColor { get; }
```

Gets the default color used in the editor for the asset. Uses the inherited default from `GameAsset` (the theme's white).

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### EditorFolder

```csharp
public override string EditorFolder { get; }
```

Groups every `CharacterAsset` under `Story > Characters` in the editor's asset tree.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FileChanged

```csharp
public bool FileChanged { get; public set; }
```

Whether this asset has been modified since it was last saved to disk. Setting this to true also invokes `OnModified`, which clears the cached `Situations`/`Data` dictionaries.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FilePath

```csharp
public string FilePath { get; public set; }
```

Path to this asset file, relative to its base directory where this asset is stored.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Guid

```csharp
public Guid Guid { get; protected set; }
```

Globally unique identifier for this character asset. Reference this GUID (never the mutable `Name`) from anything that needs to point at this character (dialogue triggers, `Owner` references from other characters, etc.).

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Icon

```csharp
public override char Icon { get; }
```

FontAwesome character icon displayed next to `CharacterAsset` entries in the editor's asset browser and dialogue tools.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path. Uses the inherited default (`false`) -- character assets are design-time content, not save data.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LocalizationNotes

```csharp
public readonly string LocalizationNotes;
```

Free-form notes attached to this character's script, shown to translators to give them context when localizing its dialogue lines.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Name

```csharp
public string Name { get; public set; }
```

Display name of this asset as shown in the editor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Owner

```csharp
public readonly Guid Owner;
```

GUID of the `SpeakerAsset` (or a type derived from it) that supplies this character's default name and portraits when no per-line override is set via `SetCustomPortraitAt`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Portrait

```csharp
public readonly string Portrait;
```

Portrait which will be shown by default from [CharacterAsset.Owner](../../Murder/Assets/CharacterAsset.html#owner), unless overridden for a specific line via `SetCustomPortraitAt`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Rename

```csharp
public bool Rename { get; public set; }
```

Whether the file should be renamed and the previous name deleted on next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SaveLocation

```csharp
public virtual string SaveLocation { get; }
```

The folder path where this asset is saved on disk. Uses the inherited default, based on `GameProfile.GenericAssetsPath` and `EditorFolder`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Situations

```csharp
public ImmutableDictionary<TKey, TValue> Situations { get; }
```

All of this character's `Situation`s (dialogue branches), keyed by their `Name` (maps `string` to `Situation`). Lazily built from the serialized situation list and cached until `OnModified` clears the cache. `CharacterRuntime` looks up situations here by name to start a conversation.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### StoreInDatabase

```csharp
public virtual bool StoreInDatabase { get; }
```

Whether this asset is stored following the database hierarchy. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TaggedForDeletion

```csharp
public bool TaggedForDeletion;
```

Marks this asset for removal from disk the next time the asset database saves.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Methods

#### OnModified()

```csharp
protected override void OnModified()
```

Clears the `Situations` and `Data` caches so they are rebuilt from the serialized lists on next access. Called whenever the editor marks this asset as modified.

#### Duplicate(string)

```csharp
public GameAsset Duplicate(string name)
```

Creates a deep copy of this asset with the given new name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### AssetsToBeSaved()

```csharp
public List<T> AssetsToBeSaved()
```

Returns and clears the list of dependent assets queued to be saved alongside this asset.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### GetEventInfoFlags(DialogueId)

```csharp
public LineInfoProperties GetEventInfoFlags(DialogueId id)
```

Returns the `LineInfoProperties` flags currently set for the dialogue line identified by `id`, or `LineInfoProperties.None` if no override data exists for it.

**Parameters** \
`id` [DialogueId](../../Murder/Core/Dialogs/DialogItemId.html) \

**Returns** \
[LineInfoProperties](../../Murder/Core/Dialogs/DialogItemId.html) \

#### GetSimplifiedName()

```csharp
public string GetSimplifiedName()
```

Returns the asset name stripped of any editor-folder prefix characters.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSplitNameWithEditorPath()

```csharp
public String[] GetSplitNameWithEditorPath()
```

Returns the display name split into path segments following the EditorFolder hierarchy.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Called after the asset is deserialized, override to implement custom post-deserialization logic. `CharacterAsset` uses the inherited no-op default.

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new GUID to this asset.

#### PrunUnusedComponents(IEnumerable<DialogueId>)

```csharp
public void PrunUnusedComponents(IEnumerable<T> unusedComponents)
```

Clears the ECS component override (but keeps any other override data) for each of the given `DialogueId`s. Used by the editor to prune component overrides that reference a component type that no longer exists or was removed from the graph.

**Parameters** \
`unusedComponents` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### PrunUnusedData()

```csharp
public void PrunUnusedData()
```

Removes any `Data` entries whose `LineInfo` is entirely empty (no speaker, portrait, event, or component override). Called by the editor to keep the serialized override list from accumulating stale, no-op entries as lines are edited over time.

#### SetActionAt(DialogueId, DialogAction?)

```csharp
public void SetActionAt(DialogueId id, DialogAction? action)
```

Attaches (or clears, if `action` is null) a `DialogAction` that runs before the dialogue line identified by `id` plays, creating an override entry for it if needed. Used to mutate blackboard facts or apply components as a side effect of a specific line.

**Parameters** \
`id` [DialogueId](../../Murder/Core/Dialogs/DialogItemId.html) \
`action` [DialogAction](../../Murder/Core/Dialogs/DialogAction.html) \

#### SetCustomComponentAt(DialogueId, IComponent)

```csharp
public void SetCustomComponentAt(DialogueId id, IComponent c)
```

Attaches (or replaces) an ECS component override on the dialogue line/action identified by `id`, creating an override entry for it if one doesn't exist yet. Used by the dialogue editor to let a writer trigger a gameplay component (e.g. a camera shake, a flag toggle) exactly when a specific line plays.

**Parameters** \
`id` [DialogueId](../../Murder/Core/Dialogs/DialogItemId.html) \
`c` [IComponent](../../Bang/Components/IComponent.html) \

#### SetCustomPortraitAt(DialogueId, Guid, string)

```csharp
public void SetCustomPortraitAt(DialogueId id, Guid speaker, string portrait)
```

Overrides the speaker and/or portrait shown for the dialogue line identified by `id`, creating an override entry for it if one doesn't exist yet. Use this to have a line rendered as though a different character (or a different expression/portrait of the same character) is speaking, without changing the line's owning `CharacterAsset`.

**Parameters** \
`id` [DialogueId](../../Murder/Core/Dialogs/DialogItemId.html) \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`portrait` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SetEventInfoAt(DialogueId, string)

```csharp
public void SetEventInfoAt(DialogueId id, string @event)
```

Attaches (or clears, if `event` is null) a named event to fire when the dialogue line identified by `id` plays, creating an override entry for it if needed. Used by gameplay code/systems listening for dialogue events to react to specific lines without hard-coding line indices.

**Parameters** \
`id` [DialogueId](../../Murder/Core/Dialogs/DialogItemId.html) \
`event` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SetEventInfoAt(DialogueId, LineInfoProperties)

```csharp
public void SetEventInfoAt(DialogueId id, LineInfoProperties flags)
```

Overload that replaces the `LineInfoProperties` flags (e.g. `SkipDefaultPortraitSound`) for the dialogue line identified by `id`, creating an override entry for it if needed.

**Parameters** \
`id` [DialogueId](../../Murder/Core/Dialogs/DialogItemId.html) \
`flags` [LineInfoProperties](../../Murder/Core/Dialogs/DialogItemId.html) \

#### SetSituation(Situation)

```csharp
public void SetSituation(Situation situation)
```

Replaces the existing situation that shares `situation`'s `Name` with the given value. Does nothing if no situation with that name exists yet -- use `SetSituations` to add a brand new situation to the list.

**Parameters** \
`situation` [Situation](../../Murder/Core/Dialogs/Situation.html) \

#### SetSituations(ImmutableArray<T>)

```csharp
public void SetSituations(ImmutableArray<T> situations)
```

Replaces the entire list of situations on this character, invalidating the cached `Situations` lookup and flagging the asset as changed. This is called when re-importing/updating dialogue scripts (e.g. from an external script file) with freshly parsed data.

**Parameters** \
`situations` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Track an asset such that `g` is also saved once this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### TryFetchSituation(string)

```csharp
public T? TryFetchSituation(string name)
```

Looks up a situation by its `Name`. Returns null if this character has no situation with that name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) -- a `Situation?`. \

⚡

# LocalizationAsset

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public class LocalizationAsset : GameAsset
```

The per-language string database of the game: each `LocalizationAsset` represents one locale (English, Portuguese, etc.) and stores every translated `LocalizedStringData` entry, keyed by the GUID carried by `LocalizedString`.

**Intent:** Serve as the single source of truth for one locale's text. A game registers one `LocalizationAsset` per supported language in `GameProfile.LocalizationResources`; at runtime `LocalizationServices` fetches the active asset (via `GameDataManager.Localization`) and resolves individual strings from it, falling back to the default (English) asset when a translation is missing.

**Use-case:** Use the editor's localization tooling (backed by `AddResource`, `SetResource`, `UpdateOrSetResource`) to add, translate, and prune entries. Dialogue import pipelines (e.g. the Gum-to-Murder converter) call `SetResourcesForDialogue` to keep an asset's dialogue-linked strings in sync with a character's script, and export tooling reads `Resources`/`DialogueResources` to produce CSV translation files.

**Implements:** _[GameAsset](../../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors

```csharp
public LocalizationAsset()
```

Default parameterless constructor (implicit). Creates an empty localization asset with no string entries; the editor calls this when a designer creates a new language resource, after which `Name`, `Guid` (via `MakeGuid`), and entries are populated.

### ⭐ Properties

#### CanBeCreated

```csharp
public virtual bool CanBeCreated { get; }
```

Determines if the asset can be created, override to change this capability. Not overridden here, so a `LocalizationAsset` can always be created through the editor's "new asset" flow.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeDeleted

```csharp
public virtual bool CanBeDeleted { get; }
```

Determines if the asset can be deleted, override to change this capability. Not overridden here, so localization assets can be deleted like any other asset.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeRenamed

```csharp
public virtual bool CanBeRenamed { get; }
```

Determines if the asset can be renamed, override to change this capability. Not overridden here, so localization assets can be renamed like any other asset.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeSaved

```csharp
public virtual bool CanBeSaved { get; }
```

Determines if the asset can be saved, override to change this capability. Not overridden here, so localization assets save normally.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DialogueResources

```csharp
public ImmutableArray<T> DialogueResources { get; }
```

Expose all the dialogue resources (for editor, etc.). Each entry groups the localized strings that came from one dialogue/character asset; used by the editor's localization view and by `LocalizationExporter` when producing per-dialogue CSV exports.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### EditorColor

```csharp
public virtual Vector4 EditorColor { get; }
```

Gets the default color used in the editor for the asset. Overridden here to a teal (`#34ebcf`) so localization assets are visually distinct from other asset types in the editor's asset browser.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### EditorFolder

```csharp
public virtual string EditorFolder { get; }
```

Gets the folder path in the editor where this asset is grouped. Overridden here to `"#Localization"`, placing all localization assets under a dedicated "Localization" folder with a custom icon in the editor tree.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FileChanged

```csharp
public bool FileChanged { get; public set; }
```

Indicates whether the asset has unsaved modifications. Setting it triggers `OnModified()`; the editor sets this to true whenever a translator edits a string entry, so the asset shows as dirty until saved.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FilePath

```csharp
public string FilePath { get; public set; }
```

Path to this asset file, relative to its base directory.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Guid

```csharp
public Guid Guid { get; protected set; }
```

Unique identifier for this asset, used to reference it from other assets and components. This is the GUID stored per-language in `GameProfile.LocalizationResources`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Icon

```csharp
public virtual char Icon { get; }
```

FontAwesome character icon displayed next to this asset in the editor. Overridden here to a book/translation-style glyph (``) so localization assets are recognizable at a glance in the editor tree.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path. Not overridden here, so localization assets are stored as regular content assets rather than save data.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsSavePacked

```csharp
public virtual bool IsSavePacked { get; }
```

Whether this file will be packed in the save, if `IsStoredInSaveData` is true. Not overridden here, so it has no effect since localization assets are not stored as save data.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; public set; }
```

Display name of this asset as shown in the editor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Rename

```csharp
public bool Rename { get; public set; }
```

Whether the file should be renamed and the previous name deleted on next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Resources

```csharp
public ImmutableArray<T> Resources { get; }
```

Expose all the resources (for editor, etc.). This is the full string table for this locale: every `LocalizedStringData` entry, dialogue-linked or not.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### SaveLocation

```csharp
public virtual string SaveLocation { get; }
```

The folder path where this asset is saved on disk.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### StoreInDatabase

```csharp
public virtual bool StoreInDatabase { get; }
```

Whether this asset is stored following the database hierarchy. Not overridden here, so localization assets follow the standard asset database layout.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TaggedForDeletion

```csharp
public bool TaggedForDeletion;
```

Marks this asset for removal on the next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Methods

#### OnModified()

```csharp
protected virtual void OnModified()
```

Called by the editor when the asset is modified; override to clear cached derived data. Not overridden here.

#### HasResource(Guid)

```csharp
public bool HasResource(Guid id)
```

Returns whether this asset already has an entry for the given GUID. Cheaper than `TryGetResource` when the caller only needs an existence check, e.g. before deciding whether to call `AddResource(Guid)` or create a brand-new entry.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Duplicate(string)

```csharp
public GameAsset Duplicate(string name)
```

Creates a deep copy of this asset with the given new name, assigning it a fresh GUID.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../../Murder/Assets/GameAsset.html) \

#### FetchResourcesForDialogue(Guid)

```csharp
public ImmutableArray<T> FetchResourcesForDialogue(Guid guid)
```

Expose all resources tied to a particular dialogue. Returns an empty array if no strings are linked to `guid`.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### AssetsToBeSaved()

```csharp
public List<T> AssetsToBeSaved()
```

Returns and clears the list of dependent assets queued to be saved alongside this asset (see `TrackAssetOnSave`).

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### AddResource(Guid)

```csharp
public void AddResource(Guid id)
```

Registers a reference to an existing (or brand-new) string identified by `id`, incrementing its `Counter`. This is called whenever a component or dialogue line starts pointing at a `LocalizedString` with this GUID, so the asset can track how many places use the string and know when it's safe to prune via `RemoveResource`. If no entry with this GUID exists yet, an empty one is created for it.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### AddResource(string, bool)

```csharp
public LocalizedString AddResource(string text, bool isGenerated)
```

Creates a brand-new string entry with a fresh GUID and the given text, and returns a `LocalizedString` handle pointing at it. This is how the editor mints new translatable text (e.g. when a designer types a new dialogue line): the text is stored on this asset (normally the default/English one) and the returned handle is what gets embedded in the component or dialogue asset that owns the text.

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`isGenerated` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[LocalizedString](../../../Murder/Assets/LocalizedString.html) \

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

Returns the display name split into path segments following the `EditorFolder` hierarchy.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TryGetResource(Guid)

```csharp
public T? TryGetResource(Guid id)
```

Attempts to retrieve the translated `LocalizedStringData` for the given GUID on this locale's asset. This is the core lookup used by `LocalizationServices.GetLocalizedString` to resolve a `LocalizedString` handle into displayable text; returns null when this locale has no translation for the id (the caller typically then falls back to the default locale).

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Called after deserialization; rebuilds internal lookup caches. Not overridden here — `LocalizationAsset` builds its GUID-to-index cache lazily on first access instead.

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new GUID to this asset.

#### RemoveResource(Guid, bool)

```csharp
public void RemoveResource(Guid id, bool force = false)
```

Releases a reference to the string identified by `id`, decrementing its `Counter`. Once the counter drops to zero the entry is removed entirely, which is how the editor keeps the localization asset free of orphaned strings as components/dialogue lines stop referencing them. Pass `force` to delete the entry immediately regardless of its remaining reference count.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`force` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveResourceForDialogue(Guid)

```csharp
public void RemoveResourceForDialogue(Guid dialogueAssetId)
```

Removes every string entry associated with the dialogue asset identified by `dialogueAssetId`, and drops the grouping itself from `DialogueResources`. Called when a dialogue/character asset is deleted or when its dialogue lines are about to be fully re-synced (see `SetResourcesForDialogue`), so the localization asset doesn't accumulate orphaned strings for content that no longer exists.

**Parameters** \
`dialogueAssetId` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### SetAllDialogueResources(ImmutableArray<T>)

```csharp
public void SetAllDialogueResources(ImmutableArray<T> resources)
```

Replaces this asset's entire dialogue-resource grouping table in one shot. Used when bulk-loading/importing dialogue-linked string data from a reference source.

**Parameters** \
`resources` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### SetAllResources(ImmutableArray<T>)

```csharp
public void SetAllResources(ImmutableArray<T> resources)
```

Replaces this asset's entire string table in one shot, invalidating the GUID lookup cache. Used when bulk-loading/importing data from a reference source (e.g. re-importing a CSV translation file over the editor's UI) rather than editing entries one at a time.

**Parameters** \
`resources` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### SetResource(LocalizedStringData)

```csharp
public void SetResource(LocalizedStringData value)
```

Inserts or overwrites the entry matching `value`'s GUID with the given data wholesale (text, notes, counter, generated flag included). Used by the editor when a translator directly edits a row in the localization grid, as opposed to `UpdateOrSetResource` which only touches the text/notes and preserves the existing reference counter.

**Parameters** \
`value` [LocalizedStringData](../../../Murder/Assets/Localization/LocalizedStringData.html) \

#### SetResourcesForDialogue(Guid, ImmutableArray<T>)

```csharp
public void SetResourcesForDialogue(Guid guid, ImmutableArray<T> resources)
```

Replaces the full set of string resources associated with the dialogue asset identified by `guid` with `resources`: any previously-linked string that is no longer in the new set has its reference released via `RemoveResource`. This is the method the Gum-to-Murder dialogue converter calls after re-parsing a dialogue script, so the localization asset's dialogue-linked strings stay in sync with the script's current lines whenever it's re-imported.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`resources` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Track an asset such that `g` is also saved once this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### UpdateOrSetNotes(Guid, string)

```csharp
public bool UpdateOrSetNotes(Guid id, string notes)
```

Updates only the translator notes for an existing entry, leaving its text untouched. Used internally by `UpdateOrSetResource` to propagate notes typed on a translation asset back onto the default (English) asset's matching entry, so notes stay attached to the string regardless of which locale's grid they were entered from. Returns false if no entry with this GUID exists on this asset.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`notes` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### UpdateOrSetResource(Guid, string, string)

```csharp
public bool UpdateOrSetResource(Guid id, string translated, string notes)
```

Sets the translated text and translator notes for the entry with the given `id` on this locale's asset, creating the entry if it doesn't exist yet. If `translated` is empty, the default (English) locale's text is used as a placeholder instead, so a translation asset never ends up with a blank string. This is the primary method the editor's translation grid calls when a translator types into a cell. Returns false if the default localization has no entry for `id` at all (i.e. the string doesn't really exist anywhere).

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`translated` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`notes` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡

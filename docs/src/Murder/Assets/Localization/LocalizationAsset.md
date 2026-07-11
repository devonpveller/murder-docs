# LocalizationAsset

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public class LocalizationAsset : GameAsset
```

Lookup table that maps `LocalizedString` GUIDs to their translated text for a single language.

**Intent:** Serve as the per-language string database: each `LocalizationAsset` represents one locale and stores all translated strings keyed by their source `LocalizedString.Id`.

**Use-case:** Register one `LocalizationAsset` per language in `GameProfile.LocalizationResources`. The localization service fetches the active asset and calls `GetLocalizedString` to resolve a `LocalizedString` at runtime. Use the editor helpers (`AddResource`, `SetResource`) to manage translated entries.

**Implements:** _[GameAsset](../../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors
```csharp
public LocalizationAsset()
```

### ⭐ Properties
#### CanBeCreated
```csharp
public virtual bool CanBeCreated { get; }
```

Determines if the asset can be created, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeDeleted
```csharp
public virtual bool CanBeDeleted { get; }
```

Determines if the asset can be deleted, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeRenamed
```csharp
public virtual bool CanBeRenamed { get; }
```

Determines if the asset can be renamed, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeSaved
```csharp
public virtual bool CanBeSaved { get; }
```

Determines if the asset can be saved, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### DialogueResources
```csharp
public ImmutableArray<T> DialogueResources { get; }
```

Expose all the dialogue resources (for editor, etc.).

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### EditorColor
```csharp
public virtual Vector4 EditorColor { get; }
```

Gets the default color used in the editor for the asset.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \
#### EditorFolder
```csharp
public virtual string EditorFolder { get; }
```

Gets the folder path in the editor where this asset is grouped.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FileChanged
```csharp
public bool FileChanged { get; public set; }
```

Indicates whether the asset has unsaved modifications.

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

Unique identifier for this asset, used to reference it from other assets and components.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Icon
```csharp
public virtual char Icon { get; }
```

FontAwesome character icon displayed next to this asset in the editor.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \
#### IsStoredInSaveData
```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path.

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

Expose all the resources (for editor, etc.).

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

Whether this asset is stored following the database hierarchy.

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

Called by the editor when the asset is modified; override to clear cached derived data.

#### HasResource(Guid)
```csharp
public bool HasResource(Guid id)
```

Returns true if a localized string entry with the given GUID exists in this asset.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Duplicate(string)
```csharp
public GameAsset Duplicate(string name)
```

Creates a deep copy of this asset with the given new name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../../Murder/Assets/GameAsset.html) \

#### FetchResourcesForDialogue(Guid)
```csharp
public ImmutableArray<T> FetchResourcesForDialogue(Guid guid)
```

Expose all resources tied to a particular dialogue.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### AssetsToBeSaved()
```csharp
public List<T> AssetsToBeSaved()
```

Returns and clears the list of dependent assets queued to be saved alongside this asset.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### AddResource(string, bool)
```csharp
public LocalizedString AddResource(string text, bool isGenerated)
```

Creates a new localized string entry with the given text and returns its `LocalizedString` handle.

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

Returns the display name split into path segments following the EditorFolder hierarchy.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TryGetResource(Guid)
```csharp
public T? TryGetResource(Guid id)
```

Attempts to retrieve the `LocalizedStringData` entry for the given GUID; returns null if not found.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### AfterDeserialized()
```csharp
public virtual void AfterDeserialized()
```

Called after deserialization; rebuilds internal lookup caches.

#### AddResource(Guid)
```csharp
public void AddResource(Guid id)
```

Registers or increments the reference count of a localized string entry by GUID.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### MakeGuid()
```csharp
public void MakeGuid()
```

Generates and assigns a new GUID to this asset.

#### RemoveResource(Guid, bool)
```csharp
public void RemoveResource(Guid id, bool force)
```

Removes a localized string entry by GUID. If `force` is false, only removes it when the reference count drops to zero.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`force` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetAllDialogueResources(ImmutableArray<T>)
```csharp
public void SetAllDialogueResources(ImmutableArray<T> resources)
```

Replaces the entire set of dialogue-linked resource entries.

**Parameters** \
`resources` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### SetResource(LocalizedStringData)
```csharp
public void SetResource(LocalizedStringData value)
```

Updates or inserts the localized string entry matching the GUID in `value`.

**Parameters** \
`value` [LocalizedStringData](../../../Murder/Assets/Localization/LocalizedStringData.html) \

#### SetResourcesForDialogue(Guid, ImmutableArray<T>)
```csharp
public void SetResourcesForDialogue(Guid guid, ImmutableArray<T> resources)
```

Associates the given set of localized string resources with the specified dialogue asset GUID.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`resources` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### TrackAssetOnSave(Guid)
```csharp
public void TrackAssetOnSave(Guid g)
```

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### UpdateOrSetResource(Guid, string, string)
```csharp
public void UpdateOrSetResource(Guid id, string translated, string notes)
```

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`translated` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`notes` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡
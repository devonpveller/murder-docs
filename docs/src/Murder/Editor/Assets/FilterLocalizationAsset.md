# FilterLocalizationAsset

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public class FilterLocalizationAsset : GameAsset
```

Singleton, engine-created asset holding every named localization filter for the project.

**Intent:** Each filter (see [FilteredAssetsForLocalization](../../../Murder/Editor/Assets/FilteredAssetsForLocalization.html)) is a saved selection of which assets/asset-types should be considered when exporting or importing localization strings; the editor's localization tools use [EditorSettingsAsset.LocalizationFilter](../../../Murder/Editor/Assets/EditorSettingsAsset.html#localizationfilter) to remember which one is currently active. Like [SpriteEventDataManagerAsset](../../../Murder/Editor/Assets/SpriteEventDataManagerAsset.html), there is only ever one instance per project and it is hidden from the asset browser.

**Use-case:** Fetched via `EditorLocalizationServices.GetFilterLocalizationAsset`, which lazily creates the asset (and its `"all"` default filter) the first time a project is localized. `GetLocalizationCandidates(string)` powers the localization editor's asset-selection UI, and `FetchLatestAssets()` is called to refresh candidates after the project's assets change.

**Implements:** _[GameAsset](../../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors

```csharp
public FilterLocalizationAsset()
```

Creates a new manager asset with no filters. Normally you should not call this directly -- use the editor's localization services to fetch the single project-wide instance instead of creating a competing one.

### ⭐ Properties

#### CanBeCreated

```csharp
public virtual bool CanBeCreated { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`. In practice the asset is never created from the browser because it is hidden.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeDeleted

```csharp
public virtual bool CanBeDeleted { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeRenamed

```csharp
public virtual bool CanBeRenamed { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeSaved

```csharp
public virtual bool CanBeSaved { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DefaultFilterName

```csharp
public static string DefaultFilterName;
```

Name of the built-in filter that includes every localizable asset, with no exclusions (`"all"`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### EditorColor

```csharp
public virtual Vector4 EditorColor { get; }
```

Not overridden by this type; inherits `GameAsset`'s default, which ties the icon color to `Game.Profile.Theme.White`.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### EditorFolder

```csharp
public override string EditorFolder { get; }
```

Returns [GameDataManager.HiddenAssetsRelativePath](../../../Murder/Data/GameDataManager.html#hiddenassetsrelativepath), which starts with [GameDataManager.SKIP_CHAR](../../../Murder/Data/GameDataManager.html#skip_char) so the editor's asset tree skips rendering this asset entirely.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FileChanged

```csharp
public bool FileChanged { get; set; }
```

Whether this asset has been modified since it was last saved to disk.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FilePath

```csharp
public string FilePath { get; set; }
```

Path to this asset file, relative to its base directory where this asset is stored.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Filters

```csharp
public ImmutableDictionary<string, FilteredAssetsForLocalization> Filters;
```

All saved filters for this project, keyed by filter name.

**Returns** \
[ImmutableDictionary\<string, FilteredAssetsForLocalization\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### Guid

```csharp
public Guid Guid { get; protected set; }
```

Globally unique identifier for this asset instance.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Icon

```csharp
public virtual char Icon { get; }
```

Not overridden by this type; inherits `GameAsset`'s default icon glyph. Irrelevant in practice since the asset is hidden from the browser.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public virtual bool IsStoredInSaveData { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `false`, so this asset is packed with regular game assets rather than stored alongside save data.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; set; }
```

Display name of this asset.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Rename

```csharp
public bool Rename { get; set; }
```

Whether it should rename the file and delete the previous name.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SaveLocation

```csharp
public virtual string SaveLocation { get; }
```

Not overridden by this type; inherits `GameAsset`'s default, deriving the save folder from `Game.Profile.GenericAssetsPath` combined with `EditorFolder`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### StoreInDatabase

```csharp
public virtual bool StoreInDatabase { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`.

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
protected virtual void OnModified()
```

Not overridden by this type; inherits `GameAsset`'s no-op default.

#### Duplicate(string)

```csharp
public GameAsset Duplicate(string name)
```

Create a deep copy of this asset with the given new name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../../Murder/Assets/GameAsset.html) \

#### AssetsToBeSaved()

```csharp
public List<T> AssetsToBeSaved()
```

Return the assets which will be saved with this asset. Also clears the pending list.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### FetchLatestAssets()

```csharp
public void FetchLatestAssets()
```

Re-scans the project and refreshes every filter's candidate list. Only the [DefaultFilterName](../../../Murder/Editor/Assets/FilterLocalizationAsset.html#defaultfiltername) filter defaults newly discovered assets to included; every other (custom) filter defaults them to excluded, so a developer's hand-picked subset does not silently grow every time an asset is added.

#### GetLocalizationCandidates(string)

```csharp
public ImmutableArray<(string, AssetInfoPropertiesForEditor)> GetLocalizationCandidates(string name)
```

Returns the asset-type-grouped candidate list for the filter named `name`, creating an empty filter under that name first if it does not exist yet.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) -- name of the filter to query. \

**Returns** \
[ImmutableArray\<(string, AssetInfoPropertiesForEditor)\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetOrCreate(string)

```csharp
public FilteredAssetsForLocalization GetOrCreate(string name)
```

Returns the [FilteredAssetsForLocalization](../../../Murder/Editor/Assets/FilteredAssetsForLocalization.html) registered under `name`, creating and registering a new empty one if it does not exist yet.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) -- name of the filter to fetch or create. \

**Returns** \
[FilteredAssetsForLocalization](../../../Murder/Editor/Assets/FilteredAssetsForLocalization.html) \

#### Remove(string)

```csharp
public void Remove(string name)
```

Deletes the filter registered under `name`. If it is currently the active filter ([EditorSettingsAsset.LocalizationFilter](../../../Murder/Editor/Assets/EditorSettingsAsset.html#localizationfilter)), the caller is responsible for selecting a replacement, since this method does not update that reference.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) -- name of the filter to remove. \

#### GetSimplifiedName()

```csharp
public string GetSimplifiedName()
```

Returns just the last segment of the asset's editor path -- i.e. `Name` with any leading editor-folder path stripped off.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSplitNameWithEditorPath()

```csharp
public String[] GetSplitNameWithEditorPath()
```

Returns `Name` combined with `EditorFolder` and split into path segments.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Not overridden by this type; inherits `GameAsset`'s no-op default.

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new globally unique identifier (GUID) to the object.

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Track an asset such that `g` is also saved once this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

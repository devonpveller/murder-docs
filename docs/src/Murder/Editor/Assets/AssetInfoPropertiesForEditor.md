# AssetInfoPropertiesForEditor

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public class AssetInfoPropertiesForEditor
```

Groups every asset of a single asset type (e.g. all `DialogueAsset`s) that is a candidate for a given localization filter, along with whether that whole group is currently selected for export/import.

**Intent:** Lets the localization filter editor show and toggle a whole asset type at once (e.g. "exclude all `FontAsset`s") in addition to toggling individual assets, without needing a separate data structure for the group-level checkbox.

**Use-case:** One instance exists per asset-type label inside a [FilteredAssetsForLocalization](../../../Murder/Editor/Assets/FilteredAssetsForLocalization.html)'s candidate list, returned from `FilteredAssetsForLocalization.GetLocalizationCandidates` and `FilterLocalizationAsset.GetLocalizationCandidates(string)`.

### ⭐ Constructors

```csharp
public AssetInfoPropertiesForEditor()
```

Creates a new, empty group with no assets and selected by default.

### ⭐ Properties

#### Assets

```csharp
public ImmutableArray<AssetPropertiesForEditor> Assets;
```

The individual assets of this type that are candidates for localization.

**Returns** \
[ImmutableArray\<AssetPropertiesForEditor\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### IsSelected

```csharp
public bool IsSelected;
```

Whether this entire asset-type group is toggled on in the localization filter UI.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡

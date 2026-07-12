# FilteredAssetsForLocalization

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public class FilteredAssetsForLocalization
```

One named localization filter's worth of candidate assets, grouped by asset type.

**Intent:** Scans every loaded `GameAsset` (skipping types the localization pipeline never touches, such as `SpriteAsset`/`FontAsset`, via [ShouldSkip(GameAsset)](../../../Murder/Editor/Assets/FilteredAssetsForLocalization.html#shouldskipgameasset)) and remembers which ones the developer has chosen to include or exclude, so re-scanning the project ([FetchLatestAssets(bool)](../../../Murder/Editor/Assets/FilteredAssetsForLocalization.html#fetchlatestassetsbool)) preserves prior choices instead of resetting them every time.

**Use-case:** Held per filter name inside [FilterLocalizationAsset.Filters](../../../Murder/Editor/Assets/FilterLocalizationAsset.html#filters). The localization editor calls `GetLocalizationCandidates` to render the include/exclude checkboxes, and `FetchLatestAssets` after assets are added/removed from the project to keep the candidate list up to date.

### ⭐ Methods

#### FetchLatestAssets(bool)

```csharp
public void FetchLatestAssets(bool startedEnabled)
```

Re-scans every loaded asset and rebuilds the candidate list, carrying over each asset's and asset-type group's previous include/exclude selection where it still applies. Newly discovered assets default to `startedEnabled` rather than always-on, so freshly added content does not silently get exported until the developer opts in.

**Parameters** \
`startedEnabled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) -- default `Show` value for assets that were not already tracked by this filter. \

#### GetLocalizationCandidates()

```csharp
public ImmutableArray<(string, AssetInfoPropertiesForEditor)> GetLocalizationCandidates()
```

Returns the asset-type-grouped list of localization candidates for this filter, scanning the project to build the list the first time it is called.

**Returns** \
[ImmutableArray\<(string, AssetInfoPropertiesForEditor)\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) -- pairs of asset-type name and its [AssetInfoPropertiesForEditor](../../../Murder/Editor/Assets/AssetInfoPropertiesForEditor.html) group. \

#### ShouldSkip(GameAsset)

```csharp
public static bool ShouldSkip(GameAsset asset)
```

Returns whether `asset` should be excluded from localization filter candidate lists -- either because its asset type never carries localizable text (localization, sprite, sprite-event, font and floor assets), or because its name is prefixed with [GameDataManager.SKIP_CHAR](../../../Murder/Data/GameDataManager.html#skip_char) to mark it as an engine-internal/hidden asset.

**Parameters** \
`asset` [GameAsset](../../../Murder/Assets/GameAsset.html) -- asset to test. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡

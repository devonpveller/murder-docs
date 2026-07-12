# AssetPropertiesForEditor

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public class AssetPropertiesForEditor
```

Per-asset toggle used by the localization filter editor.

**Intent:** Remembers whether a specific asset (identified by [Guid](../../../Murder/Editor/Assets/AssetPropertiesForEditor.html#guid)) should be included when exporting/importing localization strings for the currently active [FilterLocalizationAsset](../../../Murder/Editor/Assets/FilterLocalizationAsset.html) filter.

**Use-case:** Held in [AssetInfoPropertiesForEditor.Assets](../../../Murder/Editor/Assets/AssetInfoPropertiesForEditor.html#assets), one per candidate asset; toggling [Show](../../../Murder/Editor/Assets/AssetPropertiesForEditor.html#show) in the localization filter UI controls whether that asset is scanned for translatable strings.

### ⭐ Constructors

```csharp
public AssetPropertiesForEditor(Guid guid)
```

Creates a toggle for `guid`, defaulting to included (`Show` = `true`).

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) -- GUID of the asset this toggle refers to. \

### ⭐ Properties

#### Guid

```csharp
public Guid Guid;
```

GUID of the asset this toggle refers to.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Show

```csharp
public bool Show;
```

Whether this asset is included in the active localization filter.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡

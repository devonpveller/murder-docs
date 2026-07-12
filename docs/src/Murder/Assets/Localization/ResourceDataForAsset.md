# ResourceDataForAsset

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
sealed struct ResourceDataForAsset
```

Nested type declared inside [LocalizationAsset](../../../Murder/Assets/Localization/LocalizationAsset.html) (referenced elsewhere in code as `LocalizationAsset.ResourceDataForAsset`) that groups all `LocalizedDialogueData` entries belonging to a single dialogue asset.

**Intent:** This lets the localization system and export tooling answer "which strings belong to this piece of dialogue" without scanning every entry in `LocalizationAsset.Resources`, and lets `LocalizationAsset.RemoveResourceForDialogue` clean up all of a dialogue's strings at once when the dialogue asset is deleted.

**Use-case:** Returned as part of `LocalizationAsset.DialogueResources` and by `LocalizationAsset.FetchResourcesForDialogue` when the editor or export pipeline (`LocalizationExporter`) needs to enumerate all translated strings tied to a specific dialogue/character asset. Built and kept up to date by `LocalizationAsset.SetResourcesForDialogue`, which is called by the Gum-to-Murder dialogue converter whenever a character's script is re-imported.

### ⭐ Constructors

```csharp
public ResourceDataForAsset()
```

Creates an empty grouping (`DialogueResourceGuid` is `Guid.Empty`, `DataResources` is empty). Exists so the struct has a public parameterless constructor for serialization and `with`-expression defaults.

### ⭐ Properties

#### DialogueResourceGuid

```csharp
public readonly Guid DialogueResourceGuid { get; init; }
```

Which asset originated this resource and its respective strings — the GUID of the dialogue/character asset that owns the strings in `DataResources`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### DataResources

```csharp
public readonly ImmutableArray<LocalizedDialogueData> DataResources { get; init; }
```

The GUID/speaker pairs for every dialogue line that belongs to `DialogueResourceGuid`. Each entry's `LocalizedDialogueData.Guid` also exists as a normal `LocalizedStringData` entry in `LocalizationAsset.Resources` — this array just tracks the grouping and which speaker said it.

**Returns** \
[ImmutableArray\<LocalizedDialogueData\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

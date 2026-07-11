# ResourceDataForAsset

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
sealed struct ResourceDataForAsset
```

Internal struct that groups all `LocalizedStringData` resources belonging to a single dialogue asset.

**Intent:** Associate a set of localized string entries with the GUID of the dialogue asset that owns them, so the localization system can efficiently look up all strings for a given dialogue.

**Use-case:** Returned by `LocalizationAsset.FetchResourcesForDialogue` when the editor or export pipeline needs to enumerate all translated strings tied to a specific `CharacterAsset`.

### ⭐ Properties
#### DialogueResourceGuid
```csharp
public Guid DialogueResourceGuid { get; public set; }
```

The GUID of the dialogue asset (e.g. a `CharacterAsset`) that these string resources belong to.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Resources
```csharp
public ImmutableArray<T> Resources { get; public set; }
```

All localized string entries associated with the owning dialogue asset.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
# MurderAssetHelpers

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class MurderAssetHelpers
```

Extension helpers for working with game assets — resolving file-system paths, fetching portrait sprites for dialogue speakers, and converting GUID arrays to typed asset instances.

**Intent:** Centralizes asset utility operations that are needed by multiple systems (the data pipeline, the dialogue/portrait renderer) but do not belong on the asset classes themselves.

**Use-case:** Use `GetGameAssetPath` to resolve where an asset should be loaded from or saved to on disk, `ToAssetArray` to resolve a list of GUIDs (e.g. a tileset list) to typed assets, and the portrait helpers to look up the sprite/animation a dialogue `Line`'s speaker should display.

### ⭐ Methods

#### GetGameAssetPath(GameAsset)

```csharp
public string? GetGameAssetPath(this GameAsset asset)
```

Get the path to load or save `asset`. Resolution order: if `asset.FilePath` is already a rooted absolute path, returns it as-is; if the asset is stored in save data, joins it under `Game.Data.SaveBasePath`; otherwise resolves it under the game's assets-bin directory (optionally under the profile's asset-resources subfolder if `asset.StoreInDatabase`), combined with `asset.SaveLocation` and `asset.FilePath`. Returns `null` if no path can be determined.

**Parameters** \
`asset` [GameAsset](../../Murder/Assets/GameAsset.html) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetPortraitForLine(Line)

```csharp
public Portrait? GetPortraitForLine(Line line)
```

Resolves the `Portrait` that should be displayed for a dialogue `line`'s speaker: looks up the line's `Speaker` GUID as a `SpeakerAsset`, then finds the portrait named `line.Portrait` (falling back to the speaker's `DefaultPortrait` if the line doesn't specify one) in that speaker's `Portraits` map. Returns `null` if the line has no speaker, the speaker asset can't be found, no portrait name is available, or the named portrait doesn't exist on the speaker.

**Parameters** \
`line` [Line](../../Murder/Core/Dialogs/Line.html) \

**Returns** \
[Portrait?](../../Murder/Core/Dialogs/Portrait.html) \

#### GetSpriteAssetForPortrait(Portrait)

```csharp
public ValueTuple<T1, T2>? GetSpriteAssetForPortrait(Portrait portrait)
```

Resolves a `Portrait` definition's `Sprite` GUID to its loaded `SpriteAsset`, returning it together with the portrait's `AnimationId` as `(SpriteAsset Asset, string Animation)`. Returns `null` if the sprite asset can't be found. Pair this with `GetPortraitForLine` to go directly from a dialogue line to the sprite/animation that should be drawn for it.

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Dialogs/Portrait.html) \

**Returns** \
[ValueTuple\<T1, T2\>?](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### ToAssetArray(ImmutableArray<T>)

```csharp
public T[] ToAssetArray(this ImmutableArray<Guid> guids)
```

Resolves an immutable array of asset GUIDs to a typed array of loaded `GameAsset` instances of type `T`, in the same order as `guids`. Any GUID that fails to resolve to a `T` is logged as an error and left as the array's default (`null`) at that index, rather than throwing or shrinking the array — callers should be prepared for `null` entries if asset data is missing or misconfigured.

**Parameters** \
`guids` [ImmutableArray\<Guid\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[T[]](../../) \

⚡

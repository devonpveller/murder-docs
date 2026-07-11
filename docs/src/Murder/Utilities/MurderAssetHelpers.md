# MurderAssetHelpers

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class MurderAssetHelpers
```

Extension helpers for working with game assets — resolving file-system paths, fetching portrait sprites, and converting GUID arrays to typed asset instances.

**Intent:** Centralizes asset utility operations that are needed by multiple systems but do not belong on the asset classes themselves.

**Use-case:** Use `GetGameAssetPath` to build a storage path, `ToAssetArray` to resolve a list of GUIDs to typed assets, and portrait helpers to look up sprite assets for dialogue speakers.

### ⭐ Methods
#### GetGameAssetPath(GameAsset)
```csharp
public string GetGameAssetPath(GameAsset asset)
```

Get the path to load or save <paramref name="asset" />.

**Parameters** \
`asset` [GameAsset](../../Murder/Assets/GameAsset.html) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetPortraitForLine(Line)
```csharp
public T? GetPortraitForLine(Line line)
```

Returns the portrait sprite for the speaker in the given dialogue `line`, or `null` if no portrait is defined.

**Parameters** \
`line` [Line](../../Murder/Core/Dialogs/Line.html) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### GetSpriteAssetForPortrait(Portrait)
```csharp
public T? GetSpriteAssetForPortrait(Portrait portrait)
```

Retrieves the `SpriteAsset` associated with the given portrait definition, or `null` if not found.

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### ToAssetArray(ImmutableArray<T>)
```csharp
public T[] ToAssetArray(ImmutableArray<T> guids)
```

Resolves an immutable array of asset GUIDs to a typed array of loaded `GameAsset` instances.

**Parameters** \
`guids` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[T[]](../../) \



⚡
# PackedSaveAssetsData

**Namespace:** Murder.Assets.Save \
**Assembly:** Murder.dll

```csharp
public class PackedSaveAssetsData
```

Container that holds all serialized `GameAsset` instances for a single save slot, stored in a compressed file alongside the main save.

**Intent:** Persist the collection of `DynamicAsset` objects that belong to a save slot so they can be reloaded independently of the main `SaveData` payload.

**Use-case:** The save system writes a `PackedSaveAssetsData` to the `saved_assets.gz` file. Use `SaveDataInfo.GetFullPackedAssetsSavePath` to locate it on disk and deserialize it when reloading dynamic runtime assets for a given slot.

### ⭐ Constructors

```csharp
public PackedSaveAssetsData(List<T> assets)
```

**Parameters** \
`assets` [List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

### ⭐ Properties

#### Assets

```csharp
public readonly List<T> Assets;
```

The list of serialized `GameAsset` instances stored in this save slot.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### Name

```csharp
public static const string Name;
```

Filename used when writing this container to disk (`saved_assets.gz`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

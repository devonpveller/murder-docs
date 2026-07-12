# PackedGameData

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public class PackedGameData
```

This has the data regarding all assets and textures loaded in the game.

**Intent:** Bundles all serialized game assets into a single binary package for release builds, so `GameDataManager` can load the whole game's asset database from a handful of compressed files instead of thousands of individual asset files on disk.

**Use-case:** Written by the editor's pack step (see `GameDataManager_Packer`) to `data{0}.gz` files under the published content directory; `GameDataManager.LoadSaveGameDataAssetsAsync` deserializes each one via `FileManager.UnpackContent<PackedGameData>` and registers every asset in `Assets` via `AddAsset`. Game code never constructs this directly.

### ⭐ Constructors

```csharp
public PackedGameData(List<T> assets)
```

Creates a new `PackedGameData` with the provided list of game assets.

**Parameters** \
`assets` [List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

### ⭐ Properties

#### Assets

```csharp
public readonly List<T> Assets;
```

The full list of serialized `GameAsset` objects bundled in this data file.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### Name

```csharp
public static const string Name;
```

Filename format string used when writing or reading a packed data archive; formatted with the save-data index (e.g. `data0.gz`, `data1.gz`) since a game can be split across multiple `PackedGameData` files via `GameProfile`'s save-data count.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TexturesNoAtlasPath

```csharp
public ImmutableArray<T> TexturesNoAtlasPath { get; public set; }
```

Paths to textures that were not packed into any atlas and must be loaded individually.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

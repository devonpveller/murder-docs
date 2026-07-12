# PreloadPackedGameData

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public class PreloadPackedGameData
```

Contains the first batch of game assets loaded at startup, before the main content load begins, plus a count telling the loader how many `PackedGameData` files to expect afterward.

**Intent:** Holds the assets that must be available immediately on launch (e.g. loading-screen sprites, the preload atlas) before the full `PackedGameData` files are streamed in, so the engine can show something on screen while the rest of the game's content loads asynchronously in the background.

**Use-case:** Written by the editor's pack step to `preload_data.gz`. `GameDataManager.PreloadContentImpl` deserializes it synchronously via `FileManager.UnpackContent<PreloadPackedGameData>` during `PreloadContent()`, registers every asset in `Assets` via `AddAsset`, eagerly loads textures for any `SpriteAsset` found, and stores `TotalPackedData` so the subsequent async load knows how many indexed `PackedGameData` archives (`data0.gz`, `data1.gz`, ...) to load in `LoadAllAssetsAsync`.

### ⭐ Constructors

```csharp
public PreloadPackedGameData(int totalPackedData, List<T> assets)
```

Creates a new `PreloadPackedGameData` with the given preload asset list and the total number of `PackedGameData` archives that will follow it.

**Parameters** \
`totalPackedData` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`assets` [List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

### ⭐ Properties

#### Assets

```csharp
public readonly List<T> Assets;
```

The list of `GameAsset` objects included in the preload batch.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### Name

```csharp
public static const string Name;
```

Filename used for the preload archive on disk (always `preload_data.gz`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TotalPackedData

```csharp
public readonly int TotalPackedData;
```

The amount of save/game data that will be fetched, i.e. how many `PackedGameData` archives (`data{0}.gz`) exist and should be loaded during the async content-load phase. Defaults to `1` when not explicitly set by the deserialized value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

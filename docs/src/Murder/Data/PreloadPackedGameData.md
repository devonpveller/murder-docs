# PreloadPackedGameData

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public class PreloadPackedGameData
```

Contains the first batch of game assets loaded at startup, before the main content load begins.

**Intent:** Holds the assets that must be available immediately on launch (e.g. loading screens, preload sprites) before the full `PackedGameData` files are streamed in.

**Use-case:** Deserialized by `GameDataManager` during `PreloadContent()` to populate the engine with the minimum set of assets required to show a loading screen.

### ⭐ Constructors
```csharp
public PreloadPackedGameData(List<T> assets)
```
Creates a new `PreloadPackedGameData` with the provided list of preload assets.

**Parameters** \
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


⚡
# PackedGameData

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public class PackedGameData
```

This has the data regarding all assets and textures loaded in the gmae.

**Intent:** Bundles all serialized game assets into a single binary package for release builds.

**Use-case:** Created by the editor's pack step; the engine loads this file at startup instead of individual asset files in non-editor builds.

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
Filename pattern used when writing or reading the packed data archive (e.g. `data0.gz`).

**Returns** \
```csharp
public ImmutableArray<T> TexturesNoAtlasPath { get; public set; }
```
Paths to textures that were not packed into any atlas and must be loaded individually.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
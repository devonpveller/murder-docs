# PackedSoundData

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public class PackedSoundData
```

This has the data regarding all the sounds that will be loaded in the game.

**Intent:** Bundles everything the sound engine needs to boot into a single packed file: the per-platform bank list and the native plugin filenames the sound backend depends on, so a release build doesn't need the raw sound project files.

**Use-case:** Written by the editor's pack step (`EditorDataManager_Packer`), which populates `Banks` and `Plugins` from `Game.Sound.FetchAllBanks()`/`FetchAllPlugins()` and serializes the result to `sounds.gz`. `GameDataManager.LoadSoundsImplAsync` deserializes it back via `FileManager.UnpackContent<PackedSoundData>` and hands it to `Game.Sound.LoadContentAsync(data)` to initialize the sound backend. Game code does not construct this directly.

### ⭐ Constructors

```csharp
public PackedSoundData()
```

### ⭐ Properties

#### Banks

```csharp
public ImmutableDictionary<TKey, TValue> Banks { get; public set; }
```

This has all the banks used by the sound engine, sorted by the supported platform, e.g. "Desktop".

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### Name

```csharp
public static const string Name;
```

Filename used when writing or reading the packed sound archive (always `sounds.gz`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Plugins

```csharp
public ImmutableArray<T> Plugins { get; public set; }
```

Filenames of the sound-engine native plugins (e.g. FMOD codec/output plugins) that must be loaded alongside the sound banks at runtime. Populated at pack time from the active `ISoundPlayer` implementation via `FetchAllPlugins`.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

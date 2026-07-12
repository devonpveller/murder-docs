# GameDataManager

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public partial class GameDataManager : IDisposable
```

Central manager responsible for loading, caching, and providing access to all game assets, atlases, shaders, save data, sounds, and localization.

**Intent:** Acts as the single source of truth for all persistent game content at runtime — from sprite atlases to serialized world data to player save slots. The class is split across several `partial` files by concern (asset/content loading in `GameDataManager.cs`, save-slot management in `GameDataManager_Save.cs`, sound bank loading in `GameDataManager_Sound.cs`, and packed-content path resolution in `GameDataManager_Packer.cs`) but is documented here as a single type, since that is how it is used and subclassed.

**Use-case:** Access it via `Game.Data` to retrieve assets by GUID, load or save game progress, switch localization, and manage texture atlases. Games override it (assigning their subclass via `IMurderGame`) to plug in a custom `GameProfile` type, custom `SaveData`/`SaveDataInfo` types, custom shaders (`IShaderProvider`), or extra loading steps by overriding the `virtual`/`protected virtual` hooks (`LoadContentAsyncImpl`, `CreateGameProfile`, `CreateSaveDataWithVersion`, `FetchSystemsToStartWith`, etc.).

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
public GameDataManager(IMurderGame game)
```

Creates a new game data manager backed by a default `FileManager`. This is the constructor game code (or a game-specific `GameDataManager` subclass) normally calls, typically once at startup when wiring up `IMurderGame`.

**Parameters** \
`game` [IMurderGame](../../Murder/IMurderGame.html) \

```csharp
protected GameDataManager(IMurderGame game, FileManager fileManager)
```

Creates a new game data manager with an explicit `FileManager`. Exposed as `protected` so a subclass can inject a custom file manager (e.g. for tests or alternate storage backends) while still going through the same initialization path as the public constructor.

**Parameters** \
`game` [IMurderGame](../../Murder/IMurderGame.html) \
`fileManager` [FileManager](../../Murder/Serialization/FileManager.html) \

### ⭐ Properties

#### \_activeSaveData

```csharp
protected SaveData _activeSaveData;
```

Backing field for the currently loaded save run. `null` when no save has been created or loaded yet; use `ActiveSaveData` (throws) or `TryGetActiveSaveData()` (returns `null`) to read it from outside the class.

**Returns** \
[SaveData](../../Murder/Assets/SaveData.html) \

#### \_allAssets

```csharp
protected readonly Dictionary<TKey, TValue> _allAssets;
```

Maps every loaded asset's GUID directly to its `GameAsset` instance. This is the primary asset store; `_database` is a secondary index over the same instances grouped by concrete type.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### \_assetsBinDirectoryPath

```csharp
protected string _assetsBinDirectoryPath;
```

Cached path to the directory containing the packed binary asset files, computed once in `Initialize` from `_binResourcesDirectory` and `GameProfile.AssetResourcesPath`. Exposed publicly via `AssetsBinDirectoryPath`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### \_binResourcesDirectory

```csharp
protected string _binResourcesDirectory;
```

Root directory for binary resource files, defaulting to `"resources"`. Set from the `resourcesBinPath` argument passed to `Initialize`, and used to derive `_assetsBinDirectoryPath`/`_packedBinDirectoryPath`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### \_currentSaveAssets

```csharp
protected readonly ConcurrentDictionary<TKey, TValue> _currentSaveAssets;
```

Stores all the dynamic save assets (e.g. per-run generated `GameAsset` instances) tied to the current `ActiveSaveData`. Populated from the packed save-assets archive on load and mutated via `AddAssetForCurrentSave`/`RemoveAssetForCurrentSave`; serialized back out as part of `SerializeSaveAsync`.

**Returns** \
[ConcurrentDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Concurrent.ConcurrentDictionary-2?view=net-7.0) \

#### \_database

```csharp
protected readonly Dictionary<TKey, TValue> _database;
```

Maps each concrete `GameAsset` subtype to the set of GUIDs of loaded assets of that type. Lets `FilterAllAssets`/`FilterOutAssets`/`FindAllNamesForAsset`/`HasAsset<T>` answer "which assets are of type T" without scanning every loaded asset.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### \_fonts

```csharp
public ImmutableDictionary<TKey, TValue> _fonts;
```

Immutable map from font index to loaded `PixelFont` instances, populated by `TrackFont` as `FontAsset`s are loaded. Read by `GetFont`; rebuilt (via copy-on-write) rather than mutated in place so it can be read safely from the render thread while assets are still loading on a background thread.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### \_game

```csharp
protected readonly IMurderGame _game;
```

Reference to the game implementation used to provide custom game profiles, save data types, shaders (`IShaderProvider`), preferences, and localized font selection. May be `null` when a `GameDataManager` is constructed without a game hook (e.g. in tooling).

**Returns** \
[IMurderGame](../../Murder/IMurderGame.html) \

#### \_gameProfile

```csharp
protected GameProfile _gameProfile;
```

Backing field for `GameProfile`, loaded from disk (or created via `CreateGameProfile`) during `Initialize`. Accessing `GameProfile` before `Initialize` has run will assert, since this field is still `null` at that point.

**Returns** \
[GameProfile](../../Murder/Assets/GameProfile.html) \

#### \_packedGameDataDirectory

```csharp
protected static const string _packedGameDataDirectory;
```

Relative subdirectory name (`"content"`) where the published game content is expected to live, either under `[bin]/resources/content/` or `[source]/packed/content/`. Combined with `BinResourcesDirectoryPath` to build `PublishedPackedAssetsFullPath`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### \_referencedAtlases

```csharp
protected readonly HashSet<T> _referencedAtlases;
```

Tracks the names of every atlas referenced by an asset added via `AddAsset` (populated whenever a `SpriteAsset` is registered). Currently used as bookkeeping for atlas preloading; see the code for the up-to-date consumer.

**Returns** \
[HashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) \

#### \_runtimeSaveSlots

```csharp
protected readonly Dictionary<TKey, TValue> _runtimeSaveSlots;
```

The collection of save data known to exist, keyed by slot index, according to the `SaveDataTracker`. Populated by `LoadAllSaves` and consulted by `GetAllSaves`, `CanLoadSaveData`, and `LoadSaveAsCurrentSave` to decide which slots can actually be loaded from disk.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### \_skipLoadingAssetAtPaths

```csharp
protected readonly HashSet<T> _skipLoadingAssetAtPaths;
```

Perf: In order to avoid reloading assets that were generated by the importers, track which ones
were reloaded completely here.

**Returns** \
[HashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) \

#### ActiveSaveData

```csharp
public SaveData ActiveSaveData { get; }
```

The currently active save run. Throws `InvalidOperationException` (after logging an error) if no save has been created or loaded yet — use `TryGetActiveSaveData()` instead when the absence of an active save is an expected/handled case.

**Returns** \
[SaveData](../../Murder/Assets/SaveData.html) \

#### AssetsBinDirectoryPath

```csharp
public string AssetsBinDirectoryPath { get; }
```

Full path to the directory where packed binary asset files are located, derived from `_binResourcesDirectory` and `GameProfile.AssetResourcesPath` during `Initialize`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AssetsLock

```csharp
public Object AssetsLock;
```

Monitor object `AddAsset` locks on while mutating `_database`/`_allAssets`, since assets can be added concurrently while the editor (or async content loading) is running. Only relevant if you are writing code that mutates the asset tables outside of `AddAsset` itself.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

#### BinResourcesDirectoryPath

```csharp
public string BinResourcesDirectoryPath { get; }
```

Full path to the binary resources directory, used to locate shaders, fonts, and atlases.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### CachedUniqueTextures

```csharp
public readonly CacheDictionary<TKey, TValue> CachedUniqueTextures;
```

LRU cache (capacity 32) of individually loaded `Texture2D` objects that are not part of any atlas, populated and read by `FetchTexture`. Cleared via `ClearUniqueTextures`, which disposes every cached texture first.

**Returns** \
[CacheDictionary\<TKey, TValue\>](../../Murder/Utilities/CacheDictionary-2.html) \

#### CallAfterLoadContent

```csharp
public bool CallAfterLoadContent;
```

Set to `true` by `LoadContentAsync` once the full asynchronous content pipeline finishes; the game loop polls this (or the equivalent) to know when it is safe to call `AfterContentLoadedFromMainThread` on the main/render thread, since texture/font preloading must happen there.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CurrentGameVersion

```csharp
public virtual float CurrentGameVersion { get; }
```

The current game version, sourced from `IMurderGame.Version` (or `1` if no game hook is set). Compared against a save slot's stored version in `LoadAllSaves` to skip loading saves from an older, incompatible version.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### CurrentLocalization

```csharp
public LanguageIdData CurrentLocalization { get; private set; }
```

The language currently in effect, defaulting to `Languages.English` until `ChangeLanguage` is called (which `LoadContentAsync` does automatically at startup using the player's saved preference).

**Returns** \
[LanguageIdData](../../Murder/Assets/Localization/LanguageIdData.html) \

#### CurrentPalette

```csharp
public ImmutableArray<T> CurrentPalette;
```

Used by the color picker to allow selecting common colors quicker.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### CustomGameShaders

```csharp
public Effect[] CustomGameShaders;
```

Custom optional game shaders, provided by [GameDataManager.\_game](../../Murder/Data/GameDataManager.html#_game) when it implements `IShaderProvider`. Compiled/loaded by `LoadShaders` alongside the built-in `sprite2d`/`simple`/`pixel_art_murder` shaders.

**Returns** \
[Effect[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \

#### DefaultFont

```csharp
public int DefaultFont { get; }
```

Index of the default (localized) font to use for validation and fallback purposes, sourced from `IMurderGame.GetDefaultFont()` or `MurderFonts.PixelFont` when no game hook is set. Distinct from `GetFont`, which resolves a specific font index (optionally through per-language localization).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DitherTexture

```csharp
public Texture2D DitherTexture;
```

Slot for a dither-pattern texture usable by dithering-style render effects. Declared but not populated anywhere in the base engine at the time of writing — a game or renderer that wants dithering support can assign this field directly.

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### FileManager

```csharp
public readonly FileManager FileManager;
```

Provides all file I/O operations including serialization, deserialization, compression (pack/unpack), and directory management. Every disk read/write `GameDataManager` performs (assets, saves, shaders, atlases) goes through this instance.

**Returns** \
[FileManager](../../Murder/Serialization/FileManager.html) \

#### GameDirectory

```csharp
public virtual string GameDirectory { get; }
```

Directory name used for saving custom data, sourced from `IMurderGame.Name` (or `"Murder"` if no game hook is set). Forms the base of `SaveDirectory`/`SaveBasePath`; override to relocate where a game's save files live on disk.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GameProfile

```csharp
public GameProfile GameProfile { get; protected set; }
```

The active game profile containing global configuration such as window size, available systems, and localization resources. Asserts if accessed before `Initialize()` has been called.

**Returns** \
[GameProfile](../../Murder/Assets/GameProfile.html) \

#### GameProfileFileName

```csharp
public static const string GameProfileFileName;
```

Base filename (`"game_config"`, without extension) used when serializing/deserializing the `GameProfile` asset to disk, relative to `_binResourcesDirectory`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### HiddenAssetsRelativePath

```csharp
public static const string HiddenAssetsRelativePath;
```

Relative subdirectory name (`"_Hidden"`) used to store editor-only hidden assets that are skipped in release builds, in the same spirit as the `SKIP_CHAR` filename convention.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### IgnoreSerializationErrors

```csharp
public virtual bool IgnoreSerializationErrors { get; }
```

Whether we will continue trying to deserialize a file after finding an issue.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Localization

```csharp
public LocalizationAsset Localization { get; }
```

The localization asset for `CurrentLocalization`'s language, resolved via `GetLocalization`. Convenience shortcut for `GetLocalization(CurrentLocalization.Id)`.

**Returns** \
[LocalizationAsset](../../Murder/Assets/Localization/LocalizationAsset.html) \

#### LoadContentProgress

```csharp
public Task LoadContentProgress;
```

The `Task` backing the ongoing asynchronous content load kicked off by `LoadContent()`; starts as `Task.CompletedTask` and is replaced with the running load task. Check its status (or await it) to know when loading is complete.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### LoadedAtlasses

```csharp
public readonly Dictionary<TKey, TValue> LoadedAtlasses;
```

Maps atlas name strings (see `AtlasIdentifiers`) to the currently loaded `TextureAtlas` instances. Populated lazily by `FetchAtlas`/`TryFetchAtlas`; mutated by `ReplaceAtlas`/`DisposeAtlas`/`DisposeAtlases`.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### OtherEffects

```csharp
public virtual Effect[] OtherEffects { get; }
```

Additional game-specific shader effects beyond the built-in set; override to supply custom shaders that don't go through `IShaderProvider`.

**Returns** \
[Effect[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \

#### PackedBinDirectoryPath

```csharp
public string PackedBinDirectoryPath { get; }
```

Full path to the directory containing packed binary asset archives (shaders, atlases, `PackedGameData`/`PackedSoundData` files), computed from `_binResourcesDirectory` during `Initialize`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PendingSave

```csharp
public ValueTask<TResult> PendingSave;
```

The in-flight `SerializeSaveAsync` operation, if any. `QuickSave` checks this before starting a new save so a second save request while one is already writing to disk is skipped rather than racing with the first.

**Returns** \
[ValueTask\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask-1?view=net-7.0) \

#### Preferences

```csharp
public GamePreferences Preferences { get; }
```

The current player preferences (volume, language, scaling, etc.), lazily loaded from disk via `GamePreferences.TryFetchPreferences()`, falling back to `IMurderGame.CreateGamePreferences()` or a plain `new GamePreferences()`. Use `TryFetchPreferences()` instead if you need to check whether preferences have been loaded without triggering the load.

**Returns** \
[GamePreferences](../../Murder/Save/GamePreferences.html) \

#### PublishedPackedAssetsFullPath

```csharp
public virtual string PublishedPackedAssetsFullPath { get; }
```

File path of the packed contents for the released game (`BinResourcesDirectoryPath` + `_packedGameDataDirectory`). Every packed-content read (`PreloadPackedGameData`, `PackedGameData`, `PackedSoundData`) is joined against this path; override it to relocate where published content is read from.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SaveBasePath

```csharp
public string SaveBasePath { get; }
```

Save directory path used when serializing user data, computed once from `SaveDirectory` via `FileHelper.GetSaveBasePath` and cached thereafter.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SaveDirectory

```csharp
public virtual string SaveDirectory { get; }
```

Directory name used specifically for save files, sourced from `IMurderGame.SaveName` (which defaults to `IMurderGame.Name`) or `GameDirectory` if no game hook is set. Override this instead of `GameDirectory` if a game wants its saves in a different folder than its other custom data.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SerializationOptions

```csharp
public JsonSerializerOptions SerializationOptions { get; }
```

JSON serializer options configured with all Murder type converters and source-generation contexts, sourced from `IMurderGame.Options` when available. Used throughout `FileManager` for asset/save serialization.

**Returns** \
[JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

#### ShaderPixel

```csharp
public Effect ShaderPixel;
```

A shader specialized for rendering pixel art.

**Returns** \
[Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \

#### ShaderRelativePath

```csharp
protected readonly string ShaderRelativePath;
```

Format string for the relative path to compiled shader files, e.g. `"shaders/{0}.fxb"`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ShaderSimple

```csharp
public Effect ShaderSimple;
```

The cheapest and simplest shader.

**Returns** \
[Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \

#### ShaderSprite

```csharp
public Effect ShaderSprite;
```

Actually a fancy shader, has some sprite effect tools for us, like different color blending modes.

**Returns** \
[Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \

#### SKIP_CHAR

```csharp
public static const char SKIP_CHAR;
```

Assets whose filename begins with this character (`_`) are considered hidden and skipped during game loading, via `ShouldSkipAsset`.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### Tracker

```csharp
public SaveDataTracker Tracker { get; }
```

The `SaveDataTracker` recording which save slots exist and their versions; lazily loaded from disk (or created via `IMurderGame.CreateSaveTracker()`) on first access. Backs `GetAllSaves`/`LoadAllSaves` and is re-serialized by `SerializeSaveTrackerAsync` whenever a save slot changes.

**Returns** \
[SaveDataTracker](../../Murder/Assets/Save/SaveDataTracker.html) \

#### WaitPendingSaveTrackerOperation

```csharp
public bool WaitPendingSaveTrackerOperation { get; }
```

Returns `true` while a pending save-tracker write operation has not yet completed, or while the active save's world-save operation is still in flight. Poll this before an operation that must not race with an in-progress save (e.g. shutting down).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### WorldProcessor

```csharp
public WorldProcessor WorldProcessor { get; }
```

The `WorldProcessor` used to post-process a freshly instantiated world — e.g. resolving `Guid`-based entity target references (`GuidToIdTargetComponent`/`GuidToIdTargetCollectionComponent`) into runtime entity ids. Sourced from `IMurderGame.CreateWorldProcessor()`, or a default `WorldProcessor` if no game hook is set.

**Returns** \
[WorldProcessor](../../Murder/Data/Prefabs/WorldProcessor.html) \

### ⭐ Methods

#### AddAsset(T, bool)

```csharp
public void AddAsset(T asset, bool overwriteDuplicateGuids)
```

Registers a new asset in the asset database (`_allAssets`/`_database`), assigning it a GUID/name if it doesn't already have one. By default, adding an asset whose GUID already exists logs an error and is a no-op; pass `overwriteDuplicateGuids: true` to instead replace the existing entry (used by hot-reload). Also tracks the asset's atlas in `_referencedAtlases` if it is a `SpriteAsset`, and fires `OnAssetRenamedOrAddedOrDeleted`. Assets whose `StoreInDatabase` is `false` are silently skipped.

**Parameters** \
`asset` [T](../../) \
`overwriteDuplicateGuids` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AddAssetForCurrentSave(GameAsset)

```csharp
public bool AddAssetForCurrentSave(GameAsset asset)
```

Adds a dynamic asset to `_currentSaveAssets`, the pool of per-run assets tied to the active save slot (as opposed to assets loaded from the shipped `PackedGameData`). Returns `false` (and logs) if an asset with the same GUID is already tracked.

**Parameters** \
`asset` [GameAsset](../../Murder/Assets/GameAsset.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AfterContentLoadedFromMainThread()

```csharp
public virtual void AfterContentLoadedFromMainThread()
```

Called after the content was loaded back from the main thread.

#### CanLoadSaveData(int)

```csharp
public bool CanLoadSaveData(int slot)
```

Returns `true` if a save exists for the given slot in `_runtimeSaveSlots` (pass `-1` to ask "is there any save at all"). Note this only checks the in-memory tracker, not whether the packed files on disk are actually readable — `LoadSaveAsCurrentSave` performs that check.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ChangeLanguage(LanguageId)

```csharp
public void ChangeLanguage(LanguageId id)
```

Resolves `id` to a `LanguageIdData` via `Languages.TryGet` and switches to it; logs an error and does nothing if `id` is not a supported language.

**Parameters** \
`id` [LanguageId](../../Murder/Assets/Localization/LanguageId.html) \

#### ChangeLanguage(LanguageIdData)

```csharp
public void ChangeLanguage(LanguageIdData data)
```

Switches the active localization to `data`: updates `GamePreferences`, sets the thread's UI culture, updates `CurrentLocalization`, and clears the active save's formatted-text cache (since cached strings were formatted for the old language).

**Parameters** \
`data` [LanguageIdData](../../Murder/Assets/Localization/LanguageIdData.html) \

#### ClearContent()

```csharp
public void ClearContent()
```

Disposes and clears every cached unique texture and resets `_fonts`. Does **not** unload atlases or the asset database — see `DisposeAtlases`/`RemoveAsset` for those.

#### ClearUniqueTextures()

```csharp
public void ClearUniqueTextures()
```

Disposes every `Texture2D` currently held in `CachedUniqueTextures` and empties the cache. Called by `ClearContent`; call it directly if you only want to free standalone textures without touching fonts.

#### CreateGameProfile()

```csharp
protected virtual GameProfile CreateGameProfile()
```

Factory method that creates the game's configuration profile when none exists on disk yet, delegating to `IMurderGame.CreateGameProfile()`. Override in a subclass to return a custom `GameProfile` subtype.

**Returns** \
[GameProfile](../../Murder/Assets/GameProfile.html) \

#### CreateSave(int)

```csharp
public virtual SaveData CreateSave(int slot)
```

Wipes any previously active save, allocates a fresh `SaveData` for `slot` (via `CreateSaveDataWithVersion`), registers it as the active save, and returns it. Pass `-1` (the default) to auto-pick the next free slot via `GetNextAvailableSlot`.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[SaveData](../../Murder/Assets/SaveData.html) \

#### CreateSaveDataWithVersion(int)

```csharp
protected virtual SaveData CreateSaveDataWithVersion(int slot)
```

Creates an implementation of SaveData for the game.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[SaveData](../../Murder/Assets/SaveData.html) \

#### CreateTemporarySaveAsync(string)

```csharp
public ValueTask<TResult> CreateTemporarySaveAsync(string path)
```

Serializes the active save data to an arbitrary override path instead of the normal save-slot location, bypassing the pending-save/backup bookkeeping `QuickSave` does. Useful for exporting a save snapshot (e.g. for debugging or bug reports) without disturbing the player's real save slot.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ValueTask\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask-1?view=net-7.0) \

#### CreateWorldInstanceFromSave(Guid, Camera2D)

```csharp
public MonoWorld CreateWorldInstanceFromSave(Guid guid, Camera2D camera)
```

Instantiates a `MonoWorld` for the `WorldAsset` identified by `guid`. If the active save data has a persisted `SavedWorld` for that GUID, the world is rehydrated from it; otherwise a fresh instance is created from the asset's default layout. Throws if the world asset cannot be found.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`camera` [Camera2D](../../Murder/Core/Graphics/Camera2D.html) \

**Returns** \
[MonoWorld](../../Murder/Core/MonoWorld.html) \

#### DeleteAllSaves()

```csharp
public virtual void DeleteAllSaves()
```

Unloads the active save, clears every tracked save slot and the in-memory `SaveDataTracker`, then deletes the tracker file and every file under `SaveBasePath` from disk. Irreversible — intended for a "clear all save data" debug/settings option.

#### DeleteSaveAt(int)

```csharp
public virtual Task<TResult> DeleteSaveAt(int slot)
```

Deletes the save directory (or, if the slot has no dedicated directory, every file under `SaveBasePath`) for `slot`, unloads it from memory, and re-serializes the save tracker to reflect the deletion. Loads all saves first if they haven't been loaded yet. Returns `false` if `slot` is not a known save.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Task\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task-1?view=net-7.0) \

#### Dispose()

```csharp
public virtual void Dispose()
```

Releases all managed and GPU resources held by this manager (currently: disposes every loaded texture atlas via `DisposeAtlases`).

#### DisposeAtlas(string)

```csharp
public void DisposeAtlas(string atlas)
```

Unloads and disposes the `TextureAtlas` registered under `atlas` (see `AtlasIdentifiers` for the built-in names), freeing its GPU memory and removing it from `LoadedAtlasses`. A no-op if the atlas isn't currently loaded.

**Parameters** \
`atlas` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### DisposeAtlases()

```csharp
public void DisposeAtlases()
```

Unloads and disposes every currently loaded texture atlas and clears `LoadedAtlasses`. Called by `Dispose()`.

#### FetchAtlas(string, bool)

```csharp
public TextureAtlas FetchAtlas(string atlas, bool warnOnError)
```

Returns the loaded `TextureAtlas` for `atlas` (see `AtlasIdentifiers` for the built-in atlas names), loading it from disk into `LoadedAtlasses` on first access. Throws if the atlas file cannot be found or deserialized — use `TryFetchAtlas` instead when a missing atlas should be handled gracefully.

**Parameters** \
`atlas` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`warnOnError` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[TextureAtlas](../../Murder/Core/Graphics/TextureAtlas.html) \

#### FetchSystemsToStartWith()

```csharp
protected virtual ImmutableArray<T> FetchSystemsToStartWith()
```

This has the collection of systems which will be added to any world that will be created.
Used when hooking new systems into the editor.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FetchTexture(string)

```csharp
public Texture2D FetchTexture(string path)
```

Creates or fetches a unique texture from a path.
Looks for a `.qoi.gz` file first, falling back to `.png`; returns a magenta placeholder pixel and logs an error if neither exists. Results are cached in `CachedUniqueTextures`.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### FilterAllAssets(Type[])

```csharp
public ImmutableDictionary<TKey, TValue> FilterAllAssets(Type[] types)
```

Returns a dictionary of every loaded asset whose type is one of `types` (or whose base type is, for abstract asset hierarchies). Backing implementation for editor asset-browser filtering.

**Parameters** \
`types` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### FilterOutAssets(Type[])

```csharp
public ImmutableDictionary<TKey, TValue> FilterOutAssets(Type[] types)
```

Return all the assets except the ones in <paramref name="types" />.

**Parameters** \
`types` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### FindAllNamesForAsset(Type)

```csharp
public ImmutableHashSet<T> FindAllNamesForAsset(Type t)
```

Find all the assets names for an asset type <paramref name="t" />.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[ImmutableHashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \

#### GetAllAssets()

```csharp
public IEnumerable<T> GetAllAssets()
```

Returns all currently loaded assets (`_allAssets.Values`) as an unordered enumerable sequence.

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### GetAllSaves()

```csharp
public Dictionary<TKey, TValue> GetAllSaves()
```

List all the available saves within the game.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### GetAsepriteFrame(Guid)

```csharp
public AtlasCoordinates GetAsepriteFrame(Guid id)
```

Quick and dirty way to get a aseprite frame, animated when you don't want to deal with the animation system.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[AtlasCoordinates](../../Murder/Core/Graphics/AtlasCoordinates.html) \

#### GetAsset(Guid)

```csharp
public GameAsset GetAsset(Guid id)
```

Returns the loaded asset with the given GUID, throwing an `ArgumentException` if not found. Use `TryGetAsset(Guid)` when a missing asset is an expected/handled case.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### GetAsset(Guid)

```csharp
public T GetAsset(Guid id)
```

Returns the loaded asset of type `T` with the given GUID, throwing if not found — except for `T = SpriteAsset`, where a missing sprite falls back to `GameProfile.MissingImage` instead of throwing, so a bad/renamed sprite reference degrades to a visible placeholder rather than crashing.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[T](../../) \

#### GetDefaultLocalization()

```csharp
public LocalizationAsset GetDefaultLocalization()
```

Returns the English (default) localization asset regardless of the current language setting. Used as the ultimate fallback when a translation is missing for the active language.

**Returns** \
[LocalizationAsset](../../Murder/Assets/Localization/LocalizationAsset.html) \

#### GetFont(int, bool)

```csharp
public PixelFont GetFont(int index, bool cultureInvariant)
```

Returns the loaded `PixelFont` at `index`. Unless `cultureInvariant` is `true`, `index` is first passed through `IMurderGame.GetLocalizedFont` so the same logical font can resolve to a different glyph set per language (e.g. a CJK font for East Asian locales); `MurderFonts.SmallFont` is additionally coerced to `MurderFonts.PixelFont`. Falls back to any loaded font (logging an error) rather than throwing when `index` isn't found, unless no fonts are loaded at all.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`cultureInvariant` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[PixelFont](../../Murder/Core/Graphics/PixelFont.html) \

#### GetLocalization(LanguageId)

```csharp
protected virtual LocalizationAsset GetLocalization(LanguageId id)
```

Returns the localization asset for the given language identifier, falling back to English if unavailable.

**Parameters** \
`id` [LanguageId](../../Murder/Assets/Localization/LanguageId.html) \

**Returns** \
[LocalizationAsset](../../Murder/Assets/Localization/LocalizationAsset.html) \

#### GetNextAvailableSlot()

```csharp
public int GetNextAvailableSlot()
```

Find the next available save slot.
This is slighly expensive as it takes O(n) to complete, but you're only calling this once
so you're fine.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetPrefab(Guid)

```csharp
public PrefabAsset GetPrefab(Guid id)
```

Returns the `PrefabAsset` with the given GUID, throwing if not found. Shortcut for `GetAsset<PrefabAsset>(id)`.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[PrefabAsset](../../Murder/Assets/PrefabAsset.html) \

#### HasAsset(Guid)

```csharp
public bool HasAsset(Guid id)
```

Returns `true` if an asset of type `T` with the given GUID is currently loaded, checking `_database` without materializing the asset itself.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Initialize(string)

```csharp
public virtual void Initialize(string resourcesBinPath)
```

Clears `_database`/`_allAssets`, records `resourcesBinPath` as `_binResourcesDirectory`, loads (or creates) the `GameProfile`, and computes `_assetsBinDirectoryPath`/`_packedBinDirectoryPath`. Must be called before `GameProfile`, `AssetsBinDirectoryPath`, or `PackedBinDirectoryPath` are accessed.

**Parameters** \
`resourcesBinPath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### InitShaders()

```csharp
public virtual void InitShaders()
```

Hook invoked once during `LoadContent()`, before `PreloadContent()`. The base implementation does nothing; override to warm up any shader-related state before the main shader load pass (`LoadShaders`) runs.

#### IsPathOnSkipLoading(string)

```csharp
public bool IsPathOnSkipLoading(string name)
```

Returns `true` if `name` contains any path previously registered via `SkipLoadingAssetsAt`, meaning it should not be reloaded on hot-reload. Called from `ShouldSkipAsset`.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LoadAllAssetsAsync()

```csharp
protected virtual Task LoadAllAssetsAsync()
```

Loads every indexed `PackedGameData` archive (`data0.gz`, `data1.gz`, ... up to the count recorded in `PreloadPackedGameData.TotalPackedData`) concurrently via `LoadSaveGameDataAssetsAsync`, and awaits them all.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### LoadAllSaves()

```csharp
public bool LoadAllSaves()
```

Populates `_runtimeSaveSlots` from the `SaveDataTracker`, skipping entries whose recorded version is older than `CurrentGameVersion` or whose packed file no longer exists on disk. A no-op (returns `true` immediately) if saves were already loaded; call `ReloadAllSaves()` to force a re-scan.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LoadContent()

```csharp
public virtual void LoadContent()
```

Entry point for the full content-load sequence: clears `_database`, calls `InitShaders()` and `PreloadContent()` synchronously, then kicks off `LoadContentAsync()` on a background task and stores it in `LoadContentProgress`.

#### LoadContentAsync()

```csharp
protected Task LoadContentAsync()
```

Orchestrates the full asynchronous content load pipeline: runs `LoadContentAsyncImpl()` (subclass hook), then `LoadSoundsAsync`, `LoadAllAssetsAsync`, and `LoadFontsAndTexturesAsync` concurrently, then `LoadAllSaves()` and `ChangeLanguage` to the saved preference, finally setting `CallAfterLoadContent = true`.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### LoadContentAsyncImpl()

```csharp
protected virtual Task LoadContentAsyncImpl()
```

Override point for subclasses to execute custom async content loading logic before the built-in sounds/assets/fonts loading starts.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### LoadFontsAndTexturesAsync()

```csharp
protected virtual Task LoadFontsAndTexturesAsync()
```

Override point for loading font assets and standalone textures that are not part of any atlas; the base implementation is a no-op, since font tracking happens via `TrackFont` as `FontAsset`s are encountered during `LoadAllAssetsAsync`.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### LoadSaveAsCurrentSave(int)

```csharp
public bool LoadSaveAsCurrentSave(int slot)
```

Load a save as the current save. If more than one, it will grab whatever
is first available in all saved data.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LoadSaveGameDataAssetsAsync(int)

```csharp
protected virtual Task LoadSaveGameDataAssetsAsync(int index)
```

Deserializes a single indexed `PackedGameData` archive (`data{index}.gz`) and registers every asset it contains via `AddAsset`, tracking any `FontAsset`s along the way. Called once per index by `LoadAllAssetsAsync`; throws if the expected archive file is missing.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### LoadShader(string, out Effect&, bool, bool)

```csharp
public bool LoadShader(string name, Effect& effect, bool breakOnFail, bool forceReload)
```

Loads shader `name`, first trying a compiled `.fxb` file on disk unless `forceReload` is set, then falling back to `TryCompileShader` (a subclass hook, since the base engine has no compiler). Applies the `"DefaultTechnique"` technique if present. Throws if loading fails and `breakOnFail` is `true`; otherwise returns `false`.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`effect` [Effect&](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`breakOnFail` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`forceReload` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LoadShaders(bool, bool)

```csharp
public void LoadShaders(bool breakOnFail, bool forceReload)
```

Loads the three built-in shaders (`sprite2d` → `ShaderSprite`, `simple` → `ShaderSimple`, `pixel_art_murder` → `ShaderPixel`) plus every shader declared by `IMurderGame.Shaders` (if `_game` implements `IShaderProvider`) into `CustomGameShaders`, then notifies the active render context that shaders were reloaded.

**Parameters** \
`breakOnFail` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`forceReload` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LoadSoundsAsync(bool)

```csharp
public Task LoadSoundsAsync(bool reload)
```

This will load all the sounds to the game.

**Parameters** \
`reload` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### LoadSoundsImplAsync(bool)

```csharp
protected virtual Task LoadSoundsImplAsync(bool reload)
```

Deserializes `PackedSoundData` from disk (if present) and passes it to `Game.Sound.LoadContentAsync` to initialize the active `ISoundPlayer` backend. Override to customize how sound content is loaded.

**Parameters** \
`reload` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### OnAfterPreloadLoaded()

```csharp
protected virtual void OnAfterPreloadLoaded()
```

Immediately fired once the "fast" loading finishes.

#### OnAssetLoadError(GameAsset)

```csharp
protected virtual void OnAssetLoadError(GameAsset asset)
```

Let implementations deal with a custom handling of errors.
This is called when the asset was successfully loaded but failed to fill some of its fields.

**Parameters** \
`asset` [GameAsset](../../Murder/Assets/GameAsset.html) \

#### OnAssetRenamedOrAddedOrDeleted()

```csharp
public virtual void OnAssetRenamedOrAddedOrDeleted()
```

Called when an asset is renamed, added, or deleted; use to refresh internal caches. The base implementation does nothing — this exists primarily as an editor hot-reload hook.

#### OnErrorLoadingAsset()

```csharp
public void OnErrorLoadingAsset()
```

Marks that an error occurred while loading the asset currently being deserialized, so `TryLoadAsset`/`TryLoadAssetAsync` can detect it after the fact and route the partially-loaded asset through `OnAssetLoadError`.

#### PreloadContent()

```csharp
protected void PreloadContent()
```

Runs `PreloadContentImpl()` followed by `OnAfterPreloadLoaded()`. Called synchronously (on the calling thread) from `LoadContent()`, before the async pipeline starts, so the minimum assets needed for a loading screen are available immediately.

#### PreloadContentImpl()

```csharp
protected virtual void PreloadContentImpl()
```

Deserializes `PreloadPackedGameData` from `PublishedPackedAssetsFullPath`, registers every asset it contains via `AddAsset`, records `TotalPackedData` for later use by `LoadAllAssetsAsync`, and eagerly loads textures for any `SpriteAsset` found in the preload batch. Throws if the preload archive is missing (i.e. the game was never packed).

#### PreprocessSoundFiles()

```csharp
protected virtual void PreprocessSoundFiles()
```

Implemented by custom implementations of data manager that want to do some preprocessing on the sounds.

#### PreprocessVideoFiles()

```csharp
protected virtual void PreprocessVideoFiles()
```

Implemented by custom implementations of data manager that want to do some preprocessing on video files. Declared alongside `PreprocessSoundFiles` but not currently invoked from the base sound-loading pipeline; override if a game-specific loading step needs it.

#### QuickSave()

```csharp
public void QuickSave()
```

Fire-and-forget save: if `Game.CanSave` is `false` (e.g. running with saves disabled), only the save tracker is persisted; otherwise kicks off `SerializeSaveAsync` and stores the resulting `ValueTask` in `PendingSave`. Skips starting a new save if one is already in flight.

#### ReloadAllSaves()

```csharp
public void ReloadAllSaves()
```

Unloads the active save and forces `LoadAllSaves()` to re-scan the save tracker from scratch, picking up save slots that changed on disk since the last load.

#### RemoveAsset(Guid)

```csharp
public void RemoveAsset(Guid assetGuid)
```

Remove an asset by GUID, looking up its type from the database.

**Parameters** \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RemoveAsset(Guid)

```csharp
public void RemoveAsset(Guid assetGuid)
```

Generic overload of `RemoveAsset(Guid)` that removes an asset of the known type `T` by GUID, avoiding the type lookup the non-generic overload performs.

**Parameters** \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RemoveAsset(T)

```csharp
public void RemoveAsset(T asset)
```

Removes the given asset instance from the in-memory database, looking up its GUID and concrete type from the instance itself.

**Parameters** \
`asset` [T](../../) \

#### RemoveAsset(Type, Guid)

```csharp
protected virtual void RemoveAsset(Type t, Guid assetGuid)
```

Removes the asset with the given GUID and type from `_allAssets`/`_database`, throwing an `ArgumentException` if it isn't currently tracked. Fires `OnAssetRenamedOrAddedOrDeleted`. This is the low-level removal path every other `RemoveAsset` overload funnels into.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RemoveAssetForCurrentSave(Guid)

```csharp
public bool RemoveAssetForCurrentSave(Guid guid)
```

Removes a dynamic asset by GUID from `_currentSaveAssets`; returns `true` if the asset was found and removed.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ReplaceAtlas(string, TextureAtlas)

```csharp
public void ReplaceAtlas(string atlas, TextureAtlas newAtlas)
```

Replaces the currently loaded atlas registered under `atlas` with `newAtlas`, disposing the old one first if present. Used by hot-reload to swap in a freshly re-packed atlas without restarting the game.

**Parameters** \
`atlas` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`newAtlas` [TextureAtlas](../../Murder/Core/Graphics/TextureAtlas.html) \

#### ResetActiveSave()

```csharp
public bool ResetActiveSave()
```

This resets the active save data.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ResetPreferences()

```csharp
public void ResetPreferences()
```

Resets `GamePreferences` to its defaults on disk and clears the cached `Preferences` instance so the next access reloads the freshly-reset values. Used by a "reset settings" option in a game's options menu.

#### SaveWorld(MonoWorld)

```csharp
public void SaveWorld(MonoWorld world)
```

Persists `world`'s current state into the active save slot via `SaveData.SaveAsync`, unless the corresponding `WorldAsset` is flagged `WorldFlags.NeverPersist`, in which case the call is a no-op.

**Parameters** \
`world` [MonoWorld](../../Murder/Core/MonoWorld.html) \

#### SerializeSaveAsync(string)

```csharp
protected ValueTask<TResult> SerializeSaveAsync(string overridePath)
```

Serializes the active save (and its dynamic assets) to disk, backing up any existing files first, and re-serializes the save tracker alongside it. Returns `false` without doing anything if there is no active save or another save is already in progress. Pass `overridePath` to write to a custom location (see `CreateTemporarySaveAsync`) instead of the normal save-slot path.

**Parameters** \
`overridePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ValueTask\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask-1?view=net-7.0) \

#### SerializeSaveTrackerAsync()

```csharp
protected Task SerializeSaveTrackerAsync()
```

Writes the current `_runtimeSaveSlots` state into `Tracker.Data` (unless `Game.CanSave` is `false`) and packs the tracker to disk at `SaveBasePath`. Called both by `SerializeSaveAsync` and independently whenever a save slot is created or deleted, so the tracker stays consistent even if the full save data isn't re-written.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### ShouldSkipAsset(string)

```csharp
public virtual bool ShouldSkipAsset(string fullFilename)
```

This will skip loading assets that start with a certain char. This is used to filter assets
that are only used in the editor.

**Parameters** \
`fullFilename` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SkipLoadingAssetsAt(string)

```csharp
public void SkipLoadingAssetsAt(string path)
```

Adds `path` to the skip-loading set so that hot-reload will not overwrite assets at that location.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TrackFont(FontAsset)

```csharp
protected void TrackFont(FontAsset asset)
```

Wraps `asset` in a `PixelFont` and registers it in `_fonts` under the font's index, logging an error (and skipping registration) if that index is already taken. Called automatically as `FontAsset`s are encountered during asset loading.

**Parameters** \
`asset` [FontAsset](../../Murder/Assets/Graphics/FontAsset.html) \

#### TrackOnHotReloadSprite(Action)

```csharp
public virtual void TrackOnHotReloadSprite(Action action)
```

Hook for registering a callback to be invoked when a sprite asset is hot-reloaded. The base engine implementation is a no-op; a custom `GameDataManager` (typically the editor's) overrides this to wire up live-reload notifications. Pair with `UntrackOnHotReloadSprite` to unregister.

**Parameters** \
`action` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### TryCompileShader(string, out Effect&)

```csharp
protected virtual bool TryCompileShader(string name, Effect& result)
```

Subclass hook for compiling a shader named `name` from source at runtime (the base engine ships only precompiled `.fxb` shaders and has no compiler). The base implementation always returns `false`. Called by `LoadShader` when a precompiled shader file can't be found or `forceReload` is requested.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`result` [Effect&](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryFetchAtlas(string)

```csharp
public TextureAtlas TryFetchAtlas(string atlas)
```

Returns the loaded `TextureAtlas` registered under `atlas` (see `AtlasIdentifiers`), loading it from disk on first access, or `null` if the atlas name is empty or the atlas file doesn't exist. Unlike `FetchAtlas`, never throws.

**Parameters** \
`atlas` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[TextureAtlas](../../Murder/Core/Graphics/TextureAtlas.html) \

#### TryFetchPreferences()

```csharp
public GamePreferences TryFetchPreferences()
```

Returns the currently cached `Preferences` instance without triggering a load, or `null` if preferences have not been accessed yet. Use `Preferences` instead when you want the value loaded on demand.

**Returns** \
[GamePreferences](../../Murder/Save/GamePreferences.html) \

#### TryGetActiveSaveData()

```csharp
public SaveData TryGetActiveSaveData()
```

Active saved run in the game.

**Returns** \
[SaveData](../../Murder/Assets/SaveData.html) \

#### TryGetAsset(Guid)

```csharp
public GameAsset TryGetAsset(Guid id)
```

Get a generic asset with a <paramref name="id" />.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### TryGetAsset(Guid)

```csharp
public T TryGetAsset(Guid id)
```

Returns the loaded asset of type `T` with the given GUID, or `null` if not found (or found but of a different type).

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[T](../../) \

#### TryGetAssetForCurrentSave(Guid)

```csharp
public GameAsset TryGetAssetForCurrentSave(Guid guid)
```

Retrieve a dynamic asset within the current save data based on a guid.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### TryGetPrefab(Guid)

```csharp
public PrefabAsset TryGetPrefab(Guid id)
```

Returns the `PrefabAsset` with the given GUID, or `null` if not found. Shortcut for `TryGetAsset<PrefabAsset>(id)`.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[PrefabAsset](../../Murder/Assets/PrefabAsset.html) \

#### TryLoadAsset(string, string, bool, bool)

```csharp
public GameAsset TryLoadAsset(string path, string relativePath, bool skipFailures, bool hasEditorPath)
```

Deserializes a single asset from `path`, resolves and stores its `FilePath` relative to `relativePath` (or `hasEditorPath` for assets whose editor path is already absolute), and routes it through `OnAssetLoadError` if a partial load occurred. Returns `null` on failure when `skipFailures` is `true` (the default); otherwise the deserialization exception propagates.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`relativePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`skipFailures` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`hasEditorPath` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### TryLoadAssetAsync(string, string, bool, bool)

```csharp
public Task<TResult> TryLoadAssetAsync(string path, string relativePath, bool skipFailures, bool hasEditorPath)
```

Asynchronous counterpart of `TryLoadAsset`, deserializing via `FileManager.DeserializeAssetAsync` instead of the synchronous path.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`relativePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`skipFailures` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`hasEditorPath` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Task\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task-1?view=net-7.0) \

#### UnloadActiveSave()

```csharp
public void UnloadActiveSave()
```

Removes the active save's slot from `_runtimeSaveSlots`, clears `_currentSaveAssets`, and nulls out the active save reference, resetting the manager to the "no save loaded" state. Called by `CreateSave`/`ReloadAllSaves` before establishing a new active save.

#### UnloadCurrentSave()

```csharp
protected bool UnloadCurrentSave()
```

Lower-level counterpart of `UnloadActiveSave()`: performs the same cleanup but returns `false` instead of doing nothing when there is no active save, so callers like `ResetActiveSave` can distinguish "there was nothing to unload" from "unloaded successfully".

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### UntrackOnHotReloadSprite(Action)

```csharp
public virtual void UntrackOnHotReloadSprite(Action action)
```

Unregisters a callback previously registered via `TrackOnHotReloadSprite`. The base implementation is a no-op, matching `TrackOnHotReloadSprite`.

**Parameters** \
`action` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

⚡

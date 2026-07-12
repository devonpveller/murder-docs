# EditorSettingsAsset

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public class EditorSettingsAsset : GameAsset
```

Stores all editor-specific configuration for a Murder project: import/tool paths, hot-reload toggles, window/camera placement, per-stage and per-world editor view state, favorites, recently-used assets, and quick-test hooks.

**Intent:** Acts as the single persistent settings file for the editor itself (as opposed to `GameProfile`, which configures the shipped game). It is a singleton `GameAsset` -- `CanBeCreated`, `CanBeDeleted` and `CanBeRenamed` are all overridden to `false` -- so there is always exactly one, found and loaded automatically by the editor at startup.

**Use-case:** Accessed throughout `Murder.Editor` via `Architect.EditorSettings`; serialized alongside save data (`IsStoredInSaveData` is `true`) rather than as a packed game asset, so editor preferences persist between sessions without shipping in the game build. Individual features read and write specific fields directly, e.g. `Stage` persists camera state into `StageInfo`, `WorldAssetEditor_Selector` persists group visibility into `WorldAssetInfo`, and `EditorScene` reads `FavoriteAssets`/`CachedFavoriteAssets` to render the favorites shortcut list.

**Implements:** _[GameAsset](../../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors

```csharp
public EditorSettingsAsset(string name, string gameSourcePath)
```

Deserialization constructor invoked by the JSON serializer when loading the editor settings file from disk. You should not normally construct this by hand -- the editor creates and persists the single project-wide instance automatically the first time it runs.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`gameSourcePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) -- path to the game's source directory, used to derive [SourcePackedPath](../../../Murder/Editor/Assets/EditorSettingsAsset.html#sourcepackedpath), [SourceResourcesPath](../../../Murder/Editor/Assets/EditorSettingsAsset.html#sourceresourcespath) and [RawResourcesPath](../../../Murder/Editor/Assets/EditorSettingsAsset.html#rawresourcespath). \

### ⭐ Properties

#### AlwaysBuildAtlasOnStartup

```csharp
public bool AlwaysBuildAtlasOnStartup;
```

When `true`, the texture packer rebuilds every atlas from scratch on editor startup instead of only the atlases whose source images changed since the last pack.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AssetNamePattern

```csharp
public string AssetNamePattern;
```

Format string applied when renaming a newly duplicated asset (default `" ({0})"`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AutomaticallyHotReloadAssets

```csharp
public bool AutomaticallyHotReloadAssets;
```

When `true`, the editor automatically hot-reloads ECS asset JSON files when the editor window regains focus, instead of requiring a manual reimport.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AutomaticallyHotReloadLocalizationChanges

```csharp
public bool AutomaticallyHotReloadLocalizationChanges;
```

When `true`, the editor automatically applies changes made to localization resources without a full restart.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AutomaticallyHotReloadShaderChanges

```csharp
public bool AutomaticallyHotReloadShaderChanges;
```

When `true`, the editor will automatically recompile and reload shaders on change without a full restart.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### BinResourcesPath

```csharp
public string BinResourcesPath;
```

This points to the directory in the bin path.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### CachedFavoriteAssets

```csharp
public List<GameAsset> CachedFavoriteAssets { get; }
```

Resolves [FavoriteAssets](../../../Murder/Editor/Assets/EditorSettingsAsset.html#favoriteassets) (a set of GUIDs) into the actual `GameAsset` instances, caching the result until the number of favorites changes. Used by the editor's asset browser to render the "favorites" shortcut list without re-resolving every GUID on every frame.

**Returns** \
[List\<GameAsset\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### CanBeCreated

```csharp
public override bool CanBeCreated { get; }
```

Returns `false`; this is a project singleton and cannot be created from the asset browser.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeDeleted

```csharp
public override bool CanBeDeleted { get; }
```

Returns `false`; this asset must not be deleted from within the editor.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeRenamed

```csharp
public override bool CanBeRenamed { get; }
```

Returns `false`; this asset has a fixed name and cannot be renamed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeSaved

```csharp
public virtual bool CanBeSaved { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`, so editor settings are always eligible to be serialized to disk.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CheckForPackedAssetsIntegrity

```csharp
public bool CheckForPackedAssetsIntegrity;
```

When `true`, the editor validates that every packed asset on disk matches its expected hash/integrity signature on startup, flagging assets that were corrupted or manually edited outside the pipeline.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DefaultFloor

```csharp
public Guid DefaultFloor;
```

The default floor tiles to use when creating a new room.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### DpiScale

```csharp
public float DpiScale;
```

Additional UI scaling factor applied on top of the OS-reported DPI, letting the developer fine-tune the editor UI size independently of [FontScale](../../../Murder/Editor/Assets/EditorSettingsAsset.html#fontscale).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### EditorColor

```csharp
public virtual Vector4 EditorColor { get; }
```

Not overridden by this type; inherits `GameAsset`'s default, which ties the icon color to `Game.Profile.Theme.White`.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### EditorFolder

```csharp
public virtual string EditorFolder { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of an empty string. In practice this asset is never listed in the browser at all, since it cannot be created, deleted or renamed.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### EnableDialogueHotReload

```csharp
public bool EnableDialogueHotReload;
```

When `true`, the editor will automatically apply any changes made to dialogue files without a full restart.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FavoriteAssets

```csharp
public ImmutableHashSet<Guid> FavoriteAssets { get; }
```

GUIDs of assets the developer has starred as favorites in the asset browser, for quick access. Mutate this via [FavoriteAsset(Guid)](../../../Murder/Editor/Assets/EditorSettingsAsset.html#favoriteassetguid) and [UnfavoriteAsset(Guid)](../../../Murder/Editor/Assets/EditorSettingsAsset.html#unfavoriteassetguid) rather than modifying the underlying set directly.

**Returns** \
[ImmutableHashSet\<Guid\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \

#### FileChanged

```csharp
public bool FileChanged { get; set; }
```

Whether this asset has been modified since it was last saved to disk. Setting this to `true` (as the editor does on any edit) also invokes `OnModified` so subclasses can clear derived caches.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FilePath

```csharp
public string FilePath { get; set; }
```

Path to this asset file, relative to its base directory where this asset is stored.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FontScale

```csharp
public float FontScale;
```

Scaling factor applied to the editor's ImGui font; useful for making the UI readable on high-DPI displays.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### FxcPath

```csharp
public string? FxcPath;
```

Custom path to the FXC shader compiler executable (`fxc.exe`), used instead of the one bundled with the Windows SDK when compiling HLSL shaders. Leave `null` to use the default lookup.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GameSourcePath

```csharp
public string GameSourcePath;
```

Path to the source game directory. This expects a raw resources directory (`../../resources`), a resources directory (`resources`) and a packed directory (`packed`) beneath it -- see [SourcePackedPath](../../../Murder/Editor/Assets/EditorSettingsAsset.html#sourcepackedpath), [SourceResourcesPath](../../../Murder/Editor/Assets/EditorSettingsAsset.html#sourceresourcespath) and [RawResourcesPath](../../../Murder/Editor/Assets/EditorSettingsAsset.html#rawresourcespath).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Guid

```csharp
public Guid Guid { get; protected set; }
```

Globally unique identifier for this asset. Always store and compare the `Guid`, never the mutable `Name` or `FilePath`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Icon

```csharp
public override char Icon { get; }
```

Gear icon (FontAwesome ``) used to represent this asset wherever it might be listed.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### IgnoredTexturePackingExtensions

```csharp
public string IgnoredTexturePackingExtensions;
```

Comma-separated list of file extensions (default `.clip,.psd,.gitkeep`) that the texture packer should skip when scanning raw resource folders for images to include in an atlas.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public override bool IsStoredInSaveData { get; }
```

Returns `true`; editor settings are stored alongside save data rather than as a packed game asset.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LastHotReloadImport

```csharp
public DateTime LastHotReloadImport;
```

The time of the last resource import with hot reload.

**Returns** \
[DateTime](https://learn.microsoft.com/en-us/dotnet/api/System.DateTime?view=net-7.0) \

#### LastImported

```csharp
public DateTime LastImported;
```

The time of the last resource import.

**Returns** \
[DateTime](https://learn.microsoft.com/en-us/dotnet/api/System.DateTime?view=net-7.0) \

#### LastMetadataImported

```csharp
public DateTime LastMetadataImported;
```

The time of the last resource import with the event manager.

**Returns** \
[DateTime](https://learn.microsoft.com/en-us/dotnet/api/System.DateTime?view=net-7.0) \

#### LastOpenedAsset

```csharp
public T? LastOpenedAsset;
```

The asset currently being shown in the editor scene.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) -- a `Guid?`. \

#### LastPlayedGameMode

```csharp
public Guid LastPlayedGameMode;
```

GUID of the game mode (or save slot/profile) that was last played from the editor's quick-test menu.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### LocalizationFilter

```csharp
public Guid LocalizationFilter;
```

GUID of the [FilterLocalizationAsset](../../../Murder/Editor/Assets/FilterLocalizationAsset.html) currently selected as the "active" filter in the localization editor, controlling which assets are offered as translation candidates.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Monitor

```csharp
public int Monitor;
```

Index of the monitor the editor window should appear on when opening.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### MuteEditorSounds

```csharp
public bool MuteEditorSounds;
```

When `true`, suppresses sound effects normally played by the editor itself (e.g. UI cosmetic sounds), without affecting audio played by the game being edited.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; set; }
```

Display name of the asset as shown in the editor's asset browser and used to derive its file name on disk.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### NewAssetDefaultName

```csharp
public string NewAssetDefaultName;
```

Format string for the default name given to newly created assets (default `"New {0}"`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### OpenedTabs

```csharp
public Guid[] OpenedTabs;
```

Array of GUIDs identifying the assets that were open in the editor tabs at last save.

**Returns** \
[Guid[]](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### QuickStartScene

```csharp
public Guid QuickStartScene;
```

GUID of the world asset the editor will jump straight into when the developer presses Shift+F5, skipping the game's normal startup/menu flow.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RawResourcesPath

```csharp
public virtual string RawResourcesPath { get; }
```

This points to the resources raw path, before we get to process the contents to [SourceResourcesPath](../../../Murder/Editor/Assets/EditorSettingsAsset.html#sourceresourcespath). Computed as `GameSourcePath/../../resources`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Rename

```csharp
public bool Rename { get; set; }
```

Whether it should rename the file and delete the previous name.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SaveDeserializedAssetOnError

```csharp
public bool SaveDeserializedAssetOnError;
```

Whether an asset should be overwritten (by a save) after an error loading it, useful for recovering/normalizing an asset file that failed to deserialize cleanly.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SaveLocation

```csharp
public override string SaveLocation { get; }
```

Returns `string.Empty`; the editor settings file is written at the root of the save directory rather than under a sub-folder.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SourcePackedPath

```csharp
public virtual string SourcePackedPath { get; }
```

This points to the packed directory which will be synchronized in source. Computed as `GameSourcePath/packed`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SourceResourcesPath

```csharp
public virtual string SourceResourcesPath { get; }
```

This points to the resources which will be synchronized in source. Computed as `GameSourcePath/resources`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### StageInfo

```csharp
public readonly Dictionary<Guid, PersistStageInfo> StageInfo;
```

Last-known camera position, viewport size, zoom and debug overlay flags for each editor stage, keyed by the stage's asset/world GUID. Written whenever the developer navigates a stage view, and read when reopening the same asset so the camera resumes where it left off instead of resetting to the origin.

**Returns** \
[Dictionary\<Guid, PersistStageInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### StartMaximized

```csharp
public bool StartMaximized;
```

When `true`, the editor window will open maximized.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### StoreInDatabase

```csharp
public override bool StoreInDatabase { get; }
```

Returns `false`; editor settings are not tracked in the main game asset database.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TaggedForDeletion

```csharp
public bool TaggedForDeletion;
```

Marks this asset for removal from disk the next time the asset database saves, instead of deleting the file immediately when the user requests deletion in the editor.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TestStartDay

```csharp
public T? TestStartDay;
```

Optional override for the in-game "day" value applied when quick-testing a scene from the editor.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) -- an `int?`. \

#### TestStartTime

```csharp
public T? TestStartTime;
```

Optional override for the in-game start time (e.g. time-of-day) applied when quick-testing a scene from the editor.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) -- a `float?`. \

#### TestWorldPosition

```csharp
public T? TestWorldPosition;
```

This is a property used when creating hooks within the editor to quickly test a scene.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) -- a `Point?`. \

#### WasdCameraSpeed

```csharp
public float WasdCameraSpeed;
```

Movement speed of the editor stage camera when panning with WASD keys, in pixels per second.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### WindowSize

```csharp
public Point WindowSize;
```

Stored size of the editor window; used to restore window dimensions on next launch.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### WindowStartPosition

```csharp
public Point WindowStartPosition;
```

Stored top-left position of the editor window; used to restore window position on next launch.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### WorldAssetInfo

```csharp
public readonly Dictionary<Guid, PersistWorldStageInfo> WorldAssetInfo;
```

Persisted locked/hidden entity-group visibility state for each world asset, keyed by world GUID. Lets the world editor remember which groups the developer had hidden or locked from selection the last time they had that world open.

**Returns** \
[Dictionary\<Guid, PersistWorldStageInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

### ⭐ Methods

#### OnModified()

```csharp
protected virtual void OnModified()
```

Not overridden by this type; inherits `GameAsset`'s no-op default, since `EditorSettingsAsset` has no derived caches that need to be invalidated on edit.

#### Duplicate(string)

```csharp
public GameAsset Duplicate(string name)
```

Create a deep copy of this asset with the given new name. The copy is assigned a brand new `Guid` via `MakeGuid`, so it is treated as a distinct asset from the original.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../../Murder/Assets/GameAsset.html) \

#### AssetsToBeSaved()

```csharp
public List<T> AssetsToBeSaved()
```

Return the assets which will be saved with this asset (see `TrackAssetOnSave`). Also clears the pending list, so calling this twice in a row returns null the second time.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### FavoriteAsset(Guid)

```csharp
public void FavoriteAsset(Guid guid)
```

Marks the asset identified by `guid` as a favorite, so it appears in the editor's favorites shortcut list. Invalidates the [CachedFavoriteAssets](../../../Murder/Editor/Assets/EditorSettingsAsset.html#cachedfavoriteassets) cache.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### GetSimplifiedName()

```csharp
public string GetSimplifiedName()
```

Returns just the last segment of `GetSplitNameWithEditorPath` -- i.e. `Name` with any leading editor-folder path stripped off.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSplitNameWithEditorPath()

```csharp
public String[] GetSplitNameWithEditorPath()
```

Returns `Name` combined with `EditorFolder` and split into path segments, used by the editor to render this asset at the correct place in its folder tree.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetTimesOpenedAsset(Guid)

```csharp
public int GetTimesOpenedAsset(Guid guid)
```

Returns how many times the asset identified by `guid` has been opened in the editor, or zero if it has never been opened (or was evicted from the tracked list). Used to rank assets by "most frequently used" in the asset browser and quick-open menus.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### IncrementTimesOpenedAsset(Guid)

```csharp
public void IncrementTimesOpenedAsset(Guid guid)
```

Increments the times-opened counter for `guid`. The tracked dictionary is capped at 120 entries; once full, the least-opened asset is evicted to make room for a newly-opened one.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Not overridden by this type; inherits `GameAsset`'s no-op default.

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new globally unique identifier (GUID) to the object.

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Track an asset such that `g` is also saved once this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### UnfavoriteAsset(Guid)

```csharp
public void UnfavoriteAsset(Guid guid)
```

Removes the asset identified by `guid` from the favorites list. Invalidates the [CachedFavoriteAssets](../../../Murder/Editor/Assets/EditorSettingsAsset.html#cachedfavoriteassets) cache.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

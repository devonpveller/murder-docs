# GameProfile

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public partial class GameProfile : GameAsset
```

Represents the game profile asset containing configuration and resource paths.

**Intent:** Serve as the single root configuration asset for the entire game: define resource directory layout, the starting scene, frame-rate/vsync/collision tuning, localization resources, and default editor visual settings (theme, editor sprite GUIDs). A game has exactly one `GameProfile`, and its `FilePath` is pinned to a well-known file name (`GameDataManager.GameProfileFileName`) by the constructor.

**Use-case:** Access via `Game.Profile` at runtime to read game-wide settings such as `TargetFps`, `StartingScene`, `DefaultGridCellSize`, or `Theme`. Most of its fields are edited through the editor's game profile inspector rather than in code. It is declared `partial` in source, though at present all of its members live in a single file.

**Implements:** _[GameAsset](../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors

```csharp
public GameProfile()
```

Creates a new profile and pins its `FilePath` to the well-known game config file name, since a game has exactly one `GameProfile`.

### ⭐ Properties

#### AssetResourcesPath

```csharp
public readonly string AssetResourcesPath;
```

Root path where our data .json files are stored (`assets/`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AtlasFolderName

```csharp
public readonly string AtlasFolderName;
```

Where our atlas .png and .json files are stored, under `packed/ -> bin/resources/atlas/`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### BackColor

```csharp
public Color BackColor;
```

Background color for the game, used to clear the screen behind any rendered content.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### CanBeCreated

```csharp
public override bool CanBeCreated { get; }
```

Always `false` -- a `GameProfile` cannot be created from the editor's "new asset" flow, since a game has exactly one profile that already exists.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeDeleted

```csharp
public override bool CanBeDeleted { get; }
```

Always `false` -- the game profile cannot be deleted from the editor.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeRenamed

```csharp
public override bool CanBeRenamed { get; }
```

Always `false` -- the game profile cannot be renamed from the editor.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeSaved

```csharp
public virtual bool CanBeSaved { get; }
```

Determines if the asset can be saved, override to change this capability. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ContentAsepritePath

```csharp
public readonly string ContentAsepritePath;
```

Where our aseprite contents are stored, under `packed/ -> bin/resources/aseprite/`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ContentECSPath

```csharp
public readonly string ContentECSPath;
```

Where our ECS (world/prefab) assets are stored, under `resources/assets/ecs/`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### DefaultGridCellSize

```csharp
public readonly int DefaultGridCellSize;
```

Default cell size, in pixels, used to build the game's grid configuration on startup. Individual worlds/maps can still use a different tile size.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DefaultPalette

```csharp
public readonly string DefaultPalette;
```

Path (relative to the resources folder) of the palette texture used for palette-based color grading/shaders when no other palette is specified. Defaults to `images/murder_palette`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### DialoguesPath

```csharp
public readonly string DialoguesPath;
```

Where our dialogue contents are stored, under `packed/ -> bin/resources/dialogues/`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### EditorAssets

```csharp
public readonly EditorAssets EditorAssets;
```

GUIDs of the built-in sprites used exclusively by the Murder editor (cursors, dialogue node icons, panel backgrounds). See `EditorAssets`.

**Returns** \
[EditorAssets](../../Murder/Assets/EditorAssets.html) \

#### EditorColor

```csharp
public virtual Vector4 EditorColor { get; }
```

Gets the default color used in the editor for this asset. Uses the inherited default (`Game.Profile.Theme.White`).

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### EditorFolder

```csharp
public virtual string EditorFolder { get; }
```

Gets the folder path in the editor where this asset is grouped. Uses the inherited default (empty).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FileChanged

```csharp
public bool FileChanged { get; public set; }
```

Whether this asset has unsaved modifications.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FilePath

```csharp
public string FilePath { get; public set; }
```

Path to this asset file, relative to its base directory. Pinned by the constructor to `GameDataManager.GameProfileFileName`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FontPath

```csharp
public readonly string FontPath;
```

Legacy resource path constant left over from an earlier folder layout. Its value points at the shaders folder (`shaders/`) rather than fonts, and no code in the engine currently reads it -- font lookups use `FontsPath` instead. Kept only for backwards compatibility with old `game_config` files.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FontsPath

```csharp
public readonly string FontsPath;
```

Where our font (.ttf) contents are stored, under `packed/ -> bin/resources/fonts/`. Used by the font importer to locate raw font sources and packed font atlases.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GenericAssetsPath

```csharp
public readonly string GenericAssetsPath;
```

Where our generic (non-ECS) assets are stored, under `resources/assets/data/`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Guid

```csharp
public Guid Guid { get; protected set; }
```

Unique identifier for this asset, used to reference it from other assets and components.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### HiResPath

```csharp
public readonly string HiResPath;
```

Where our high resolution image contents are stored, under `packed/ -> bin/resources/hires_images/`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Icon

```csharp
public override char Icon { get; }
```

FontAwesome character icon displayed next to the game profile entry in the editor.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### InputGraphics

```csharp
public readonly Guid InputGraphics;
```

GUID of the `InputGraphicsAsset` that supplies the button/key icon sprites shown when rendering input prompts (e.g. "Press [A]") for the currently active input device.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### InputProfile

```csharp
public readonly Guid InputProfile;
```

GUID of the `InputProfileAsset` that defines the default button bindings registered with the input system on startup.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### IsSavePacked

```csharp
public virtual bool IsSavePacked { get; }
```

Whether this file will be packed in the save, if `IsStoredInSaveData` is true. Uses the inherited default (`false`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path. Uses the inherited default (`false`) -- the game profile is design-time content, not save data.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsVSyncEnabled

```csharp
public readonly bool IsVSyncEnabled;
```

Whether vertical synchronization is enabled; turning this off might cause a lot of tearing.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LocalizationPath

```csharp
public readonly string LocalizationPath;
```

Where our localization assets are stored, under `root/resources` (`loc/`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### LocalizationResources

```csharp
public ImmutableDictionary<TKey, TValue> LocalizationResources;
```

Dictionary mapping languages to the appropriate `LocalizationAsset` resource IDs (maps `LanguageId` to `Guid`). `LocalizationServices` uses this to find the correct localization asset for the player's selected language.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### MinimumVelocityForSweep

```csharp
public readonly int MinimumVelocityForSweep;
```

Distance threshold, in pixels per frame, above which the physics system performs an additional swept collision check to avoid tunneling through thin colliders at high speed.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### MissingImage

```csharp
public readonly Guid MissingImage;
```

ID of the default image used when an image is missing.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Name

```csharp
public string Name { get; public set; }
```

Display name of this asset as shown in the editor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PreloadTextures

```csharp
public readonly bool PreloadTextures;
```

Whether textures (e.g. fonts) should be preloaded. If true, startup time might be slower but the actual game will be faster.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PushAwayInterval

```csharp
public readonly float PushAwayInterval;
```

Reserved for a minimum interval, in seconds, between push-away collision resolution passes. Currently only serialized as part of the profile and not read anywhere in the engine.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Rename

```csharp
public bool Rename { get; public set; }
```

Whether the file should be renamed and the previous name deleted on next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SaveLocation

```csharp
public override string SaveLocation { get; }
```

Always empty -- the game profile is not stored under the generic assets hierarchy like other assets; it is saved directly via its pinned `FilePath`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ScalingFilter

```csharp
public bool ScalingFilter { get; }
```

Whether texture scaling smoothing (bilinear filtering) is applied when the game is scaled to fit the window/screen.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ShadersPath

```csharp
public readonly string ShadersPath;
```

Where our compiled shader (.fx) contents are stored, under `packed/ -> bin/resources/shaders/`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SkipDirectoryIconCharacter

```csharp
public static const char SkipDirectoryIconCharacter;
```

Marker character (`#`) that, when placed at the start of an `EditorFolder` path segment, suppresses the folder's default icon in the editor tree.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### SoundsPath

```csharp
public readonly string SoundsPath;
```

Where our sound contents are stored, under `packed/ -> bin/resources/sounds/`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### StartingScene

```csharp
public readonly Guid StartingScene;
```

GUID of the `WorldAsset` that is loaded automatically when the game first starts.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### StoreInDatabase

```csharp
public override bool StoreInDatabase { get; }
```

Always `false` -- the single game profile is not stored following the generic multi-asset database hierarchy.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TaggedForDeletion

```csharp
public bool TaggedForDeletion;
```

Marks this asset for removal on the next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TargetFps

```csharp
public readonly int TargetFps;
```

Desired frame rate for the fixed and render update loops; the game loop targets this many frames per second.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### TextIcons

```csharp
public readonly Guid TextIcons;
```

GUID of the `TextIconsAsset` supplying icons used for rendering inline icon glyphs in game text.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Theme

```csharp
public readonly Theme Theme;
```

Color palette used by the editor UI and any in-game elements that pull from theme colors (e.g. debug rendering, editor gizmos); override individual fields to reskin the editor.

**Returns** \
[Theme](../../Murder/Assets/Theme.html) \

#### VideoPath

```csharp
public readonly string VideoPath;
```

Where our video contents are stored, under `packed/ -> bin/resources/video/`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### OnModified()

```csharp
protected virtual void OnModified()
```

Called by the editor when the asset is modified. `GameProfile` uses the inherited no-op default.

#### Duplicate(string)

```csharp
public GameAsset Duplicate(string name)
```

Creates a deep copy of this asset with the given new name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### AssetsToBeSaved()

```csharp
public List<T> AssetsToBeSaved()
```

Returns and clears the list of dependent assets queued to be saved alongside this asset.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### GetSimplifiedName()

```csharp
public string GetSimplifiedName()
```

Returns the asset name stripped of any editor-folder prefix characters.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSplitNameWithEditorPath()

```csharp
public String[] GetSplitNameWithEditorPath()
```

Returns the display name split into path segments following the EditorFolder hierarchy.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Called after deserialization. `GameProfile` uses the inherited no-op default.

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new GUID to this asset.

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Queues a dependent asset by GUID to be saved whenever this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

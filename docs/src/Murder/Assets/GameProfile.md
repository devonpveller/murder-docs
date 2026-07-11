# GameProfile

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class GameProfile : GameAsset
```

Represents the game profile asset containing configuration and resource paths.

**Intent:** Serve as the single root configuration asset for the entire game: define viewport dimensions, asset directory paths, the starting scene, localization resources, and editor visual settings.

**Use-case:** Access via `Game.Profile` at runtime to read game-wide settings such as `GameWidth`, `GameHeight`, `StartingScene`, or `Theme`. Override fields in the editor to configure a new game project without touching code.

**Implements:** _[GameAsset](../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors
```csharp
public GameProfile()
```

### ⭐ Properties
#### Aspect
```csharp
public float Aspect { get; }
```

Gets the game's intended aspect ratio

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### AssetResourcesPath
```csharp
public readonly string AssetResourcesPath;
```

Root path where our data .json files are stored.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### AtlasFolderName
```csharp
public readonly string AtlasFolderName;
```

Where our atlas .png and .json files are stored.
            Under: 
              packed/ -&gt; bin/resources/
                atlas/

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### BackColor
```csharp
public Color BackColor;
```

Background color for the game.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \
#### CanBeCreated
```csharp
public virtual bool CanBeCreated { get; }
```

Determines if the asset can be created, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeDeleted
```csharp
public virtual bool CanBeDeleted { get; }
```

Determines if the asset can be deleted, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeRenamed
```csharp
public virtual bool CanBeRenamed { get; }
```

Determines if the asset can be renamed, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeSaved
```csharp
public virtual bool CanBeSaved { get; }
```

Determines if the asset can be saved, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### ContentAsepritePath
```csharp
public readonly string ContentAsepritePath;
```

Where our aseprite contents are stored.
            Under:
              packed/ -&gt; bin/resources/
                aseprite/

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### ContentECSPath
```csharp
public readonly string ContentECSPath;
```

Where our ecs assets are stored.
            Under:
              resources/
                assets/
                  ecs/

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### DefaultGridCellSize
```csharp
public readonly int DefaultGridCellSize;
```

Default grid cell size in pixels used by the world editor's tile grid.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### DialoguesPath
```csharp
public readonly string DialoguesPath;
```

Where our dialogues contents are stored.
            Under:
              packed/ -&gt; bin/resources/
                dialogues/

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### EditorAssets
```csharp
public readonly EditorAssets EditorAssets;
```

Collection of sprite GUIDs used by the editor UI (cursors, dialogue icons, box backgrounds).

**Returns** \
[EditorAssets](../../Murder/Assets/EditorAssets.html) \
#### EditorColor
```csharp
public virtual Vector4 EditorColor { get; }
```

Gets the default color used in the editor for this asset.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \
#### EditorFolder
```csharp
public virtual string EditorFolder { get; }
```

Gets the folder path in the editor where this asset is grouped.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Exploration
```csharp
public readonly Exploration Exploration;
```

Configuration for the map exploration/fog-of-war system, including tint colors and animation durations.

**Returns** \
[Exploration](../../Murder/Assets/Exploration.html) \
#### FeedbackKey
```csharp
public readonly string FeedbackKey;
```

API key used to authenticate feedback or bug-report submissions.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FeedbackUrl
```csharp
public readonly string FeedbackUrl;
```

Used for reporting bugs and feedback.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FileChanged
```csharp
public bool FileChanged { get; public set; }
```

Indicates whether the asset has unsaved modifications.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### FilePath
```csharp
public string FilePath { get; public set; }
```

Path to this asset file, relative to its base directory.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FixedUpdateFactor
```csharp
public readonly float FixedUpdateFactor;
```

Multiplier applied to the fixed-update timestep, allowing the physics/game simulation to run slower or faster.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### FontPath
```csharp
public readonly string FontPath;
```

Where our font contents are stored.
            Under:
              packed/ -&gt; bin/resources/
                fonts/

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FontsPath
```csharp
public readonly string FontsPath;
```

Where our sound contents are stored.
            Under:
              packed/ -&gt; bin/resources/
                fonts/

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Fullscreen
```csharp
public bool Fullscreen;
```

Whether the game starts in fullscreen mode.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### GameHeight
```csharp
public readonly int GameHeight;
```

Game desired display height. Use [RenderContext.Camera](../../Murder/Core/Graphics/RenderContext.html#camera) size for the runtime value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### GameScale
```csharp
public readonly float GameScale;
```

Game scaling factor.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### GameWidth
```csharp
public readonly int GameWidth;
```

Game desired display width. Use [RenderContext.Camera](../../Murder/Core/Graphics/RenderContext.html#camera) size for the runtime value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### GenericAssetsPath
```csharp
public readonly string GenericAssetsPath;
```

Where our generic assets are stored.
            Under:
              resources/
                assets/
                  data/

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

Where our high resolution contents are stored.
            Under:
              packed/ -&gt; bin/resources
                shaders/

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Icon
```csharp
public virtual char Icon { get; }
```

FontAwesome character icon displayed next to this asset in the editor.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \
#### IsStoredInSaveData
```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsVSyncEnabled
```csharp
public readonly bool IsVSyncEnabled;
```

Whether vertical synchronization is enabled; turning this off may cause screen tearing.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### LocalizationPath
```csharp
public readonly string LocalizationPath;
```

Where our localization assets are stored.
            Under:
              root/resources

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### LocalizationResources
```csharp
public ImmutableDictionary<TKey, TValue> LocalizationResources;
```

Dictionary mapping languages to the appropriate localization asset resource IDs.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
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
public bool PreloadTextures;
```

Whether textures (e.g. fonts) should be preloaded. If true, startup time might be slower but
            actual game will be faster.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### PushAwayInterval
```csharp
public readonly float PushAwayInterval;
```

Minimum time interval in seconds between successive push-away collision resolution steps.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Rename
```csharp
public bool Rename { get; public set; }
```

Whether the file should be renamed and the previous name deleted on next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### ResizeStyle
```csharp
public readonly ViewportResizeStyle ResizeStyle;
```

**Returns** \
[ViewportResizeStyle](../../Murder/Core/Graphics/ViewportResizeStyle.html) \
#### SaveLocation
```csharp
public virtual string SaveLocation { get; }
```

The folder path where this asset is saved on disk.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### ScalingFilter
```csharp
public bool ScalingFilter { get; }
```

Texture scaling smoothing

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### ShadersPath
```csharp
public readonly string ShadersPath;
```

Where our aseprite contents are stored.
            Under:
              packed/ -&gt; bin/resources/
                shaders/

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### ShowUiDebug
```csharp
public readonly bool ShowUiDebug;
```

When true, enables UI debug overlays showing layout bounds and widget identifiers.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### SoundsPath
```csharp
public readonly string SoundsPath;
```

Where our sound contents are stored.
            Under:
              packed/ -&gt; bin/resources/
                sounds/

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### StartingScene
```csharp
public readonly Guid StartingScene;
```

GUID of the `WorldAsset` that is loaded when the game first starts.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### StoreInDatabase
```csharp
public virtual bool StoreInDatabase { get; }
```

Whether this asset is stored following the database hierarchy.

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

Desired frame rate; the game loop targets this many frames per second.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Theme
```csharp
public readonly Theme Theme;
```

The color palette used by the editor and in-game UI; override to apply a custom visual theme.

**Returns** \
[Theme](../../Murder/Assets/Theme.html) \
### ⭐ Methods
#### OnModified()
```csharp
protected virtual void OnModified()
```

Called by the editor when the asset is modified; override to clear cached derived data.

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

Called after deserialization; override to rebuild caches from deserialized data.

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
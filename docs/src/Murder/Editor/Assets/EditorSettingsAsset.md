# EditorSettingsAsset

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public class EditorSettingsAsset : GameAsset
```

Stores all editor-specific configuration for a Murder project, including source paths, tool paths, and editor UI preferences.

**Intent:** Acts as the persistent settings file for the editor, holding everything from the Aseprite executable path to which world was last open.

**Use-case:** Accessed via `Game.EditorSettings` inside the editor; serialized automatically alongside other editor-only save data so preferences persist between sessions.

**Implements:** _[GameAsset](../../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors
```csharp
public EditorSettingsAsset(string name, string gameSourcePath, ImmutableArray<T> editorSystems)
```

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`gameSourcePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`editorSystems` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### AlwaysBuildAtlasOnStartup
```csharp
public bool AlwaysBuildAtlasOnStartup;
```
When `true`, the editor will always rebuild all texture atlases on startup regardless of file timestamps.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### AsepritePath
```csharp
public string AsepritePath;
```
Absolute path to the Aseprite executable used for sprite import and hot-reload.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### AssetNamePattern
```csharp
public string AssetNamePattern;
```
Format string applied when renaming a newly duplicated asset (e.g. `" ({0})"`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### AutomaticallyHotReloadDialogueChanges
```csharp
public bool AutomaticallyHotReloadDialogueChanges;
```
When `true`, the editor will automatically reimport dialogue files on change without a full restart.

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
#### CameraPositions
```csharp
public readonly Dictionary<TKey, TValue> CameraPositions;
```
Persists the last known camera position for each open editor stage, keyed by stage/world GUID.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### CanBeCreated
```csharp
public virtual bool CanBeCreated { get; }
```
Returns `false`; this asset is a singleton and cannot be created from the asset browser.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeDeleted
```csharp
public virtual bool CanBeDeleted { get; }
```
Returns `false`; this asset must not be deleted from within the editor.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeRenamed
```csharp
public virtual bool CanBeRenamed { get; }
```
Returns `false`; this asset has a fixed name and cannot be renamed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeSaved
```csharp
public virtual bool CanBeSaved { get; }
```
Returns `true`; the editor settings asset is always serialized to disk.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### DefaultFloor
```csharp
public Guid DefaultFloor;
```

The default floor tiles to use when creating a new room.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### EditorColor
```csharp
public virtual Vector4 EditorColor { get; }
```
Color used to tint this asset's icon in the editor asset browser.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \
#### EditorFolder
```csharp
public virtual string EditorFolder { get; }
```
The virtual folder path that groups this asset in the editor asset browser.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### EditorSystems
```csharp
public ImmutableArray<T> EditorSystems { get; }
```

These are all the systems the editor currently supports.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### FileChanged
```csharp
public bool FileChanged { get; public set; }
```
Dirty flag indicating that this asset has been modified and needs to be saved.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### FilePath
```csharp
public string FilePath { get; public set; }
```
Absolute path to the serialized file on disk for this asset.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FontScale
```csharp
public float FontScale;
```
Scaling factor applied to editor UI fonts; useful for high-DPI displays.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### FxcPath
```csharp
public string FxcPath;
```
Path to the FXC shader compiler executable used to compile HLSL shaders for DirectX.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### GameSourcePath
```csharp
public string GameSourcePath;
```

This points to the packed directory which will be synchronized in source.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Guid
```csharp
public Guid Guid { get; protected set; }
```
Unique identifier for this asset.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Icon
```csharp
public virtual char Icon { get; }
```
Icon character from the icon font used to represent this asset in the editor browser.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \
#### IgnoredTexturePackingExtensions
```csharp
public string IgnoredTexturePackingExtensions;
```
Comma-separated list of file extensions (e.g. `.clip,.psd`) that the atlas packer should skip.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### IsStoredInSaveData
```csharp
public virtual bool IsStoredInSaveData { get; }
```
Returns `true`; editor settings are stored alongside save data rather than packed assets.

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

The time of the last resource import with event manager.

**Returns** \
[DateTime](https://learn.microsoft.com/en-us/dotnet/api/System.DateTime?view=net-7.0) \
#### LastOpenedAsset
```csharp
public T? LastOpenedAsset;
```

The asset currently being shown in the editor scene.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### LuaScriptsPath
```csharp
public string LuaScriptsPath;
```
Path to the directory containing Lua scripts used by editor tools and importers.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Monitor
```csharp
public int Monitor;
```
Index of the monitor the editor window should appear on when `StartMaximized` is false.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Name
```csharp
public string Name { get; public set; }
```
Display name of this asset as shown in the editor asset browser.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### NewAssetDefaultName
```csharp
public string NewAssetDefaultName;
```
Format string for the default name given to newly created assets (e.g. `"New {0}"`).

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
GUID of the world asset that will be loaded when the developer presses Shift+F5 for a quick play test.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### RawResourcesPath
```csharp
public string RawResourcesPath { get; }
```

This points to the resources raw path, before we get to process the contents to [EditorSettingsAsset.SourceResourcesPath](../../../Murder/Editor/Assets/EditorSettingsAsset.html#sourceresourcespath).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Rename
```csharp
public bool Rename { get; public set; }
```
Indicates whether this asset is currently in a rename operation in the editor.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### SaveAsepriteInfoOnSpriteAsset
```csharp
public bool SaveAsepriteInfoOnSpriteAsset;
```
When `true`, saves raw Aseprite metadata alongside the generated sprite asset.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### SaveDeserializedAssetOnError
```csharp
public bool SaveDeserializedAssetOnError;
```
When `true`, writes the partially-deserialized asset back to disk when a deserialization error occurs, aiding debugging.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### SaveLocation
```csharp
public virtual string SaveLocation { get; }
```
Relative directory where this asset is serialized; empty string means root save directory.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### SourcePackedPath
```csharp
public string SourcePackedPath { get; }
```

This points to the packed directory which will be synchronized in source.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### SourceResourcesPath
```csharp
public string SourceResourcesPath { get; }
```

This points to the resources which will be synchronized in source.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### StartMaximized
```csharp
public bool StartMaximized;
```
When `true`, the editor window will open maximized.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### StartOnEditor
```csharp
public bool StartOnEditor;
```
When `true`, the game launches directly into the editor scene instead of the normal startup flow.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### StoreInDatabase
```csharp
public virtual bool StoreInDatabase { get; }
```
Returns `false`; editor settings are not tracked in the main asset database.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### TaggedForDeletion
```csharp
public bool TaggedForDeletion;
```
When `true`, this asset is queued for deletion on the next save operation.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### TestStartTime
```csharp
public T? TestStartTime;
```
Optional override for the game start time used when running a quick-test from the editor.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### TestStartWithEntityAndComponent
```csharp
public T? TestStartWithEntityAndComponent;
```
Optional entity and component pair used to configure a quick-test start state in the editor.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### TestWorldPosition
```csharp
public T? TestWorldPosition;
```

This is a property used when creating hooks within the editor to quickly test a scene.
            TODO: Move this to save, eventually? Especially if this is a in-game feature at some point.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### UseCustomCutscene
```csharp
public bool UseCustomCutscene;
```
When `true`, the editor uses a custom cutscene implementation instead of the default.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### WasdCameraSpeed
```csharp
public float WasdCameraSpeed;
```
Movement speed of the editor camera when navigating with WASD keys.

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
### ⭐ Methods
#### OnModified()
```csharp
protected virtual void OnModified()
```
Called whenever any property of this asset changes; override to react to settings updates.

#### Duplicate(string)
```csharp
public GameAsset Duplicate(string name)
```
Creates a deep copy of this asset with the given name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../../Murder/Assets/GameAsset.html) \

#### AssetsToBeSaved()
```csharp
public List<T> AssetsToBeSaved()
```
Returns the list of additional assets that should be saved along with this one.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### GetSimplifiedName()
```csharp
public string GetSimplifiedName()
```
Returns the asset's display name with any path prefix stripped.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSplitNameWithEditorPath()
```csharp
public String[] GetSplitNameWithEditorPath()
```
Splits the asset name into segments including the editor folder path.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AfterDeserialized()
```csharp
public virtual void AfterDeserialized()
```
Called after this asset has been deserialized; use to perform post-load initialization.

#### MakeGuid()
```csharp
public void MakeGuid()
```
Assigns a new random GUID to this asset.

#### TrackAssetOnSave(Guid)
```csharp
public void TrackAssetOnSave(Guid g)
```
Registers the asset identified by `g` to be serialized the next time this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### UpdateSystems(ImmutableArray<T>)
```csharp
public void UpdateSystems(ImmutableArray<T> systems)
```
Replaces the editor's registered systems list with the given immutable array.

**Parameters** \
`systems` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \



⚡
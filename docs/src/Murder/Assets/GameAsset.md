# GameAsset

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public abstract class GameAsset
```

The GameAsset is the core functionality on how Murder Engine serializes and persists data of the game. Its design is made so most of its data structures should be immutable while the game is running and any field modification is left to the editor project.
            You can override its fields and methods to specify where how it will be displayed in the editor, e.g.EditorFolder and EditorIcon.

**Intent:** Define the base contract for all engine data assets: a unique GUID, a display name, editor metadata, and serialization/save hooks.

**Use-case:** Subclass `GameAsset` to create custom data containers (levels, characters, configurations). Reference an asset by its `Guid` from ECS components using `AssetRef<T>` or `GameAssetId`. Use `GameData` to look up assets at runtime, and override `EditorFolder`, `EditorColor`, and `Icon` to control how the asset appears in the editor browser.

### ⭐ Constructors
```csharp
public GameAsset()
```

### ⭐ Properties
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
#### EditorColor
```csharp
public virtual Vector4 EditorColor { get; }
```

Gets the default color used in the editor for the asset, override to use a custom color. From 0 to 1.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \
#### EditorFolder
```csharp
public virtual string EditorFolder { get; }
```

Gets the default folder path in the editor for the asset, override to specify a different folder.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FileChanged
```csharp
public bool FileChanged { get; public set; }
```

Indicates whether the asset has unsaved modifications that require writing to disk.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### FilePath
```csharp
public string FilePath { get; public set; }
```

Path to this asset file, relative to its base directory where this asset is stored.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Guid
```csharp
public Guid Guid { get; protected set; }
```

Unique identifier for this asset, used to reference it from other assets and components.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Icon
```csharp
public virtual char Icon { get; }
```

Gets the icon character for the asset, override to provide a custom icon. Use a free FontAwesome character for this to work.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \
#### IsStoredInSaveData
```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is saved relative do the save path.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Name
```csharp
public string Name { get; public set; }
```

Display name of the asset shown in the editor asset browser.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Rename
```csharp
public bool Rename { get; public set; }
```

Whether it should rename the file and delete the previous name.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### SaveLocation
```csharp
public virtual string SaveLocation { get; }
```

The folder path where this asset is saved on disk; override to change the default save location.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### SkipDirectoryIconCharacter
```csharp
public static const char SkipDirectoryIconCharacter;
```

Special character that, when prefixed to an `EditorFolder` segment, suppresses the folder icon in the editor tree.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \
#### StoreInDatabase
```csharp
public virtual bool StoreInDatabase { get; }
```

Whether this file should be stored following a database hierarchy of the files.
            True by default.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### TaggedForDeletion
```csharp
public bool TaggedForDeletion;
```

Marks this asset for removal on the next save operation.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
### ⭐ Methods
#### OnModified()
```csharp
protected virtual void OnModified()
```

Implemented by assets that may cache data.
            This notifies it that it has been modified (usually by an editor).

#### Duplicate(string)
```csharp
public GameAsset Duplicate(string name)
```

Create a duplicate of the current asset.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### AssetsToBeSaved()
```csharp
public List<T> AssetsToBeSaved()
```

Return the assets which will be saved with this ([GameAsset._saveAssetsOnSave](../../Murder/Assets/GameAsset.html#_saveassetsonsave)). 
            Also clear the pending list.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### GetSimplifiedName()
```csharp
public string GetSimplifiedName()
```

Returns the asset name with any editor-folder prefix characters stripped.

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

Called after the asset is deserialized, override to implement custom post-deserialization logic.

#### MakeGuid()
```csharp
public void MakeGuid()
```

Generates and assigns a new globally unique identifier (GUID) to the object.

#### TrackAssetOnSave(Guid)
```csharp
public void TrackAssetOnSave(Guid g)
```

Track an asset such that <paramref name="g" /> is also saved once this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \



⚡
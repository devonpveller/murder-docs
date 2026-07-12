# GameAsset

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public abstract class GameAsset
```

The GameAsset is the core functionality on how Murder Engine serializes and persists data of the game. Its design is made so most of its data structures should be immutable while the game is running and any field modification is left to the editor project. You can override its fields and methods to specify how it will be displayed in the editor, e.g. `EditorFolder` and `Icon`.

**Intent:** Define the base contract for every engine data asset: a unique GUID, a display name, editor metadata (icon, folder, color), and the serialization/save hooks (`FilePath`, `FileChanged`, `Rename`, `TaggedForDeletion`, `AfterDeserialized`, `OnModified`) that the editor's asset pipeline relies on to persist assets to disk.

**Use-case:** Subclass `GameAsset` to create custom data containers (levels, characters, configurations, item definitions). Reference an asset by its `Guid` from ECS components using the `GameAssetId` attribute. Use `Game.Data` to look up assets at runtime, and override `EditorFolder`, `EditorColor`, and `Icon` to control how the asset appears in the editor's asset browser. For example:

```csharp
public class InventoryItemAsset : GameAsset
{
    public override char Icon => ''; // Custom icon for the inventory item
    public override string EditorFolder => "#Items"; // Default folder in the editor using custom icon
    public override Vector4 EditorColor => new Vector4(1, 0.5f, 0, 1); // Custom color

    public readonly string ItemName;
    public readonly float Value;
}
```

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

Gets the default color used in the editor for the asset, override to use a custom color. From 0 to 1. Defaults to `Game.Profile.Theme.White`.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### EditorFolder

```csharp
public virtual string EditorFolder { get; }
```

Gets the default folder path in the editor for the asset, override to specify a different folder. Prefix a segment with `SkipDirectoryIconCharacter` (`#`) to pair it with a custom icon glyph, e.g. `"#World"`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FileChanged

```csharp
public bool FileChanged { get; public set; }
```

Whether this asset has been modified since it was last saved to disk. Setting this to true (as the editor does on any edit) also invokes `OnModified` so subclasses can clear derived caches.

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

Globally unique identifier for this asset. This is how every other asset/component/field that references an asset does so (e.g. via `GameAssetId`) -- always store and compare the `Guid`, never the mutable `Name` or `FilePath`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Icon

```csharp
public virtual char Icon { get; }
```

Gets the icon character for the asset, override to provide a custom icon. Use a free FontAwesome character for this to work.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### IsSavePacked

```csharp
public virtual bool IsSavePacked { get; }
```

Whether this file will be packed in the save, if `IsStoredInSaveData` is true.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is saved relative to the save path.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; public set; }
```

Display name of the asset as shown in the editor's asset browser and used to derive its file name on disk. Changing this does not by itself rename the file on disk -- set `Rename` to true to persist the new name.

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

Folder (relative to the game's resources) this asset is written into when saved, derived by default from `Game.Profile.GenericAssetsPath` and this asset's `EditorFolder`. Override to place a specific asset type in a different location (e.g. alongside packed atlases).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SkipDirectoryIconCharacter

```csharp
public static const char SkipDirectoryIconCharacter;
```

Marker character (`#`) that, when placed at the start of an `EditorFolder` path segment, tells the editor's asset tree to render that segment without its usual folder icon (typically because a custom icon glyph immediately follows it).

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### StoreInDatabase

```csharp
public virtual bool StoreInDatabase { get; }
```

Whether this file should be stored following a database hierarchy of the files. True by default.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TaggedForDeletion

```csharp
public bool TaggedForDeletion;
```

Marks this asset for removal from disk the next time the asset database saves, instead of deleting the file immediately when the user requests deletion in the editor.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Methods

#### OnModified()

```csharp
protected virtual void OnModified()
```

Implemented by assets that may cache data. This notifies it that it has been modified (usually by an editor), so it can clear/rebuild any cached derived state.

#### Duplicate(string)

```csharp
public GameAsset Duplicate(string name)
```

Create a deep copy of this asset with the given new name. The copy is assigned a brand new `Guid` via `MakeGuid`, so it is treated as a distinct asset from the original.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### AssetsToBeSaved()

```csharp
public List<T> AssetsToBeSaved()
```

Return the assets which will be saved with this asset (see `TrackAssetOnSave`). Also clears the pending list, so calling this twice in a row returns null the second time.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### GetSimplifiedName()

```csharp
public string GetSimplifiedName()
```

Returns just the last segment of `GetSplitNameWithEditorPath` -- i.e. `Name` with any leading editor-folder path stripped off. Useful for showing a clean label for the asset without its folder prefix.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSplitNameWithEditorPath()

```csharp
public String[] GetSplitNameWithEditorPath()
```

Returns `Name` combined with `EditorFolder` and split into path segments, used by the editor to render this asset at the correct place in its folder tree.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Called after the asset is deserialized, override to implement custom post-deserialization logic (e.g. rebuilding a cache that isn't itself serialized).

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new globally unique identifier (GUID) to the object.

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Track an asset such that `g` is also saved once this asset is saved. Used for assets with dependents that must stay in sync, such as localization resources or a sprite event manager.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

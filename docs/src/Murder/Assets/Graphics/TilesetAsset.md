# TilesetAsset

**Namespace:** Murder.Assets.Graphics \
**Assembly:** Murder.dll

```csharp
public class TilesetAsset : GameAsset
```

Defines the visual and collision properties of a tileset texture atlas, including per-tile rendering order, collision layer, and optional auto-tile drawing helpers.

**Intent:** Package all the metadata needed to render a tileset — the source sprite, tile dimensions, draw order, sort offset, collision layer, and optional additional tile variants — into one serializable asset.

**Use-case:** Assign a `TilesetAsset` to a tile layer in the world editor. At runtime the renderer uses `DrawTile` or `CalculateAndDrawAutoTile` to blit individual cells from the tileset texture into the world with the correct sorting and collision configuration.

**Implements:** _[GameAsset](../../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors
```csharp
public TilesetAsset()
```

### ⭐ Properties
#### AdditionalTiles
```csharp
public readonly ImmutableArray<T> AdditionalTiles;
```

Optional additional `TilesetAsset` GUIDs layered on top of this tileset for richer visual variation.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
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
#### CollisionLayer
```csharp
public readonly int CollisionLayer;
```

Bit-mask collision layer assigned to tiles in this tileset, used for physics queries.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### ConsiderOutsideOccupied
```csharp
public readonly bool ConsiderOutsideOccupied;
```

When true, areas outside the map bounds are treated as occupied tiles for auto-tile edge calculations.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### EditorColor
```csharp
public virtual Vector4 EditorColor { get; }
```

Gets the default color used in the editor for the asset.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \
#### EditorFolder
```csharp
public virtual string EditorFolder { get; }
```

Gets the folder path in the editor where this asset is grouped.

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

FontAwesome character icon displayed next to this asset in the editor.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \
#### Image
```csharp
public readonly Guid Image;
```

GUID of the `SpriteAsset` whose texture atlas contains the tile frames for this tileset.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### IsStoredInSaveData
```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Name
```csharp
public string Name { get; public set; }
```

Display name of this asset as shown in the editor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Offset
```csharp
public readonly Point Offset;
```

Pixel offset applied to all tiles drawn from this tileset.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Order
```csharp
public readonly int Order;
```

This is the order (or layer) which this tileset will be drawn into the screen.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Properties
```csharp
public readonly ITileProperties Properties;
```

Optional tile behaviour properties (e.g. surface type) applied to all tiles in this tileset.

**Returns** \
[ITileProperties](../../../Murder/Core/ITileProperties.html) \
#### Rename
```csharp
public bool Rename { get; public set; }
```

Whether the file should be renamed and the previous name deleted on next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### SaveLocation
```csharp
public virtual string SaveLocation { get; }
```

The folder path where this asset is saved on disk.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Size
```csharp
public readonly Point Size;
```

Size in pixels of each tile cell in the tileset grid.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Sort
```csharp
public float Sort;
```

Base sort value used to order this tileset relative to other draw layers (0 to 1).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
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
#### TargetBatch
```csharp
public int TargetBatch;
```

The sprite batch slot this tileset is drawn into; determines layering relative to other batches.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### YSortOffset
```csharp
public readonly int YSortOffset;
```

Vertical pixel offset added to the tile's world Y position before computing its sort key.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
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
[GameAsset](../../../Murder/Assets/GameAsset.html) \

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

#### GetProperties()
```csharp
public T GetProperties()
```

Returns the tile properties cast to the requested type `T`; returns default if the type does not match.

**Returns** \
[T](../../../) \

#### AfterDeserialized()
```csharp
public virtual void AfterDeserialized()
```

Called after deserialization; override to rebuild caches from deserialized data.

#### CalculateAndDrawAutoTile(RenderContext, int, int, bool, bool, bool, bool, float, Color, Vector3)
```csharp
public void CalculateAndDrawAutoTile(RenderContext render, int x, int y, bool topLeft, bool topRight, bool botLeft, bool botRight, float alpha, Color color, Vector3 blend)
```

Selects and draws the correct auto-tile corner piece at grid position (`x`, `y`) based on the four neighbour-occupancy flags.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`topLeft` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`topRight` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`botLeft` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`botRight` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`alpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### DrawTile(Batch2D, int, int, int, int, float, Color, Vector3, float)
```csharp
public void DrawTile(Batch2D batch, int x, int y, int tileX, int tileY, float alpha, Color color, Vector3 blend, float sortAdjust)
```

Draws a single tile from the tileset at world position (`x`, `y`) using texture coordinates (`tileX`, `tileY`).

**Parameters** \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`tileX` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`tileY` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`alpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
`sortAdjust` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

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
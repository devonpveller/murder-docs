# SpriteAsset

**Namespace:** Murder.Assets.Graphics \
**Assembly:** Murder.dll

```csharp
public class SpriteAsset : GameAsset, IPreview
```

Stores the complete animation data for a sprite, including atlas coordinates for every frame, named animation sequences, and optional nine-slice rectangle.

**Intent:** Serve as the authoritative data record for a sprite: which frames exist, how they are grouped into named animations, where the sprite origin sits, and which texture atlas they live in.

**Use-case:** Reference a `SpriteAsset` GUID from a `SpriteComponent` to render an animated sprite. Call `GetFrame(int)` to get atlas coordinates for a given frame index, and inspect `Animations` to retrieve an `Animation` by name when playing a specific sequence.

**Implements:** _[GameAsset](../../../Murder/Assets/GameAsset.html), [IPreview](../../../Murder/Assets/IPreview.html)_

### ⭐ Constructors

```csharp
public SpriteAsset()
```

```csharp
public SpriteAsset(Guid guid, TextureAtlas atlas, string name, ImmutableArray<T> frames, ImmutableDictionary<TKey, TValue> animations, Point origin, Point size, Rectangle nineSlice)
```

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`atlas` [TextureAtlas](../../../Murder/Core/Graphics/TextureAtlas.html) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`frames` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`animations` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
`origin` [Point](../../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \
`nineSlice` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

```csharp
public SpriteAsset(Guid guid, string atlasId, string name, ImmutableArray<T> frames, ImmutableDictionary<TKey, TValue> animations, Point origin, Point size, Rectangle nineSlice)
```

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`atlasId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`frames` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`animations` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
`origin` [Point](../../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \
`nineSlice` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

### ⭐ Properties

#### Animations

```csharp
public ImmutableDictionary<TKey, TValue> Animations { get; private set; }
```

Named animation sequences, each mapping an animation name to its `Animation` definition (frame list, events, speed).

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### Atlas

```csharp
public readonly string Atlas;
```

Identifier (atlas ID string, e.g. `"atlas"`, `"editor"`, `"static"`) of the texture atlas that contains this sprite's frames. This is resolved at draw/load time via `Game.Data.FetchAtlas(atlasId)` to look up the actual `TextureAtlas` instance.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

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

#### Frames

```csharp
public readonly ImmutableArray<T> Frames;
```

Ordered list of atlas coordinates for each frame of this sprite.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

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

#### NineSlice

```csharp
public readonly Rectangle NineSlice;
```

Rectangle defining the nine-slice border insets for stretching this sprite without distorting its corners.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Origin

```csharp
public readonly Point Origin;
```

Pixel offset of the sprite's pivot point from the top-left corner of its bounding box.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

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

Dimensions in pixels of the sprite's bounding box.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

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

### ⭐ Methods

#### OnModified()

```csharp
protected virtual void OnModified()
```

Called by the editor when the asset is modified; clears the animation cache.

#### GetFrame(int)

```csharp
public AtlasCoordinates GetFrame(int frame)
```

Returns the atlas texture coordinates for the given frame index.

**Parameters** \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[AtlasCoordinates](../../../Murder/Core/Graphics/AtlasCoordinates.html) \

#### AddMessageToAnimationFrame(string, int, string)

```csharp
public bool AddMessageToAnimationFrame(string animationName, int frame, string message)
```

Attaches an event message string to a specific frame of the named animation; returns true if successful.

**Parameters** \
`animationName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveMessageFromAnimationFrame(string, int)

```csharp
public bool RemoveMessageFromAnimationFrame(string animationName, int frame)
```

Removes the event message from the specified frame of the named animation; returns true if a message was present.

**Parameters** \
`animationName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

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

#### GetPreviewId()

```csharp
public ValueTuple<T1, T2> GetPreviewId()
```

Implements [IPreview](../../../Murder/Assets/IPreview.html). Returns the `(Atlas, frame name)` pair identifying which atlas image to draw as this asset's thumbnail in the editor's asset browser.

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Called after deserialization; override to rebuild caches from deserialized data.

#### AppendEditorPath(string)

```csharp
public void AppendEditorPath(string prefix)
```

Set a directory prefix used for the editor folder.

**Parameters** \
`prefix` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

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

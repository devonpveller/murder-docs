# SavedWorld

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class SavedWorld : GameAsset, IWorldAsset
```

Asset for a map that has been generated within a world.

**Intent:** Store a serialized snapshot of all entity instances in a world at the time of saving, so the exact state can be restored on load.

**Use-case:** Obtained via `SaveData.TryLoadLevel`. Pass a `SavedWorld` to the world-loading pipeline to restore the saved entity layout. Call `CreateAsync` to asynchronously write the current world state into a new `SavedWorld` instance.

**Implements:** _[GameAsset](../../Murder/Assets/GameAsset.html), [IWorldAsset](../../Murder/Assets/IWorldAsset.html)_

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

#### Instances

```csharp
public ImmutableArray<T> Instances { get; }
```

GUIDs of every entity instance captured in this world snapshot. This exposes the dictionary keys only (not the `EntityInstance` values themselves) — use `TryGetInstance` to resolve a specific instance by GUID.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### IsSavePacked

```csharp
public virtual bool IsSavePacked { get; }
```

Whether this file will be packed in the save, if `IsStoredInSaveData` is true. Overridden to `true` on `SavedWorld`, since world snapshots are written into the active save slot rather than the generic asset database.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path. Overridden to `true` on `SavedWorld`, since instances live under the save slot's own directory rather than the generic asset database.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; public set; }
```

Display name of this asset as shown in the editor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### NextEligibleEntityId

```csharp
public int NextEligibleEntityId { get; }
```

The next free entity id that was not yet assigned in the world at the time this snapshot was taken. When a `WorldAsset` is instantiated from a `SavedWorld` (via `WorldAsset.CreateInstanceFromSave`), the new `MonoWorld`'s entity id counter is seeded from this value so newly spawned entities never collide with ids restored from the snapshot.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

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

#### WorldGuid

```csharp
public Guid WorldGuid { get; }
```

Implements `IWorldAsset.WorldGuid`, but always returns `Guid.Empty` for `SavedWorld` — unlike `WorldAsset`, a saved snapshot is not itself addressable by a world GUID; it is instead looked up indirectly through `SaveData.SavedWorlds` (which maps the *original* world's GUID to this snapshot's own asset `Guid`).

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

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

#### CreateAsync(World, ImmutableArray<T>)

```csharp
public static ValueTask<TResult> CreateAsync(World world, ImmutableArray<T> entitiesOnSaveRequested)
```

Static factory that asynchronously builds a brand-new `SavedWorld` snapshot from `entitiesOnSaveRequested` (typically `world.GetAllEntities()`), via an internal `SavedWorldBuilder`. This is what `SaveData.SaveAsync` calls to persist a world that should survive across runs (e.g. the city hub); the resulting `SavedWorld` is then added to `Game.Data` and tracked in `SaveData.SavedWorlds`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entitiesOnSaveRequested` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[ValueTask\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask-1?view=net-7.0) \

#### TryGetInstance(Guid)

```csharp
public EntityInstance? TryGetInstance(Guid instanceGuid)
```

Retrieves the `EntityInstance` with the given GUID from this snapshot; returns null if not found.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Called after the asset is deserialized; override to implement custom post-deserialization logic. `SavedWorld` does not override this — its internal instances cache (used by `FetchInstances`) is computed lazily on first access instead.

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

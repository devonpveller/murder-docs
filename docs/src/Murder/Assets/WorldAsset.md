# WorldAsset

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class WorldAsset : GameAsset, IWorldAsset
```

Represents a complete game level/world, storing all entity instances and their initial component data, plus the ECS systems and feature flags active in that level.

**Intent:** Act as the design-time serialized form of a full game scene: entities with their component values, grouped into editor folders, plus the system and feature configuration that governs gameplay for that world.

**Use-case:** Create one `WorldAsset` per level. Populate it in the editor with entities and features. At runtime the engine instantiates all entities and activates the configured systems; retrieve a `WorldAsset` by GUID from `Game.Data` and use `TryGetInstance` to inspect individual entity data.

**Implements:** _[GameAsset](../../Murder/Assets/GameAsset.html), [IWorldAsset](../../Murder/Assets/IWorldAsset.html)_

### ⭐ Constructors
```csharp
public WorldAsset()
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
#### Features
```csharp
public ImmutableArray<T> Features { get; }
```

The feature asset references (with active flags) assigned to this world.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
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
#### HasSystems
```csharp
public bool HasSystems { get; }
```

Returns true if this world has at least one active ECS system configured.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Icon
```csharp
public virtual char Icon { get; }
```

FontAwesome character icon displayed next to this asset in the editor.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \
#### Instances
```csharp
public virtual ImmutableArray<T> Instances { get; }
```

Ordered list of all entity instances defined in this world.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
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
#### Order
```csharp
public readonly int Order;
```

This is the order in which this world will be displayed in game (when selecting a lvel, etc.)

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
#### Systems
```csharp
public ImmutableArray<T> Systems { get; }
```

The raw ECS system type entries (with active flags) directly assigned to this world.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### TaggedForDeletion
```csharp
public bool TaggedForDeletion;
```

Marks this asset for removal on the next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### WorldGuid
```csharp
public virtual Guid WorldGuid { get; }
```

The GUID that uniquely identifies this world (same as `Guid` for `WorldAsset`).

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### WorldName
```csharp
public readonly string WorldName;
```

This is the world name used when fetching this world within the game.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### OnModified()
```csharp
protected virtual void OnModified()
```

Called by the editor when the asset is modified; clears the cached instances list.

#### PostProcessEntities(World, Dictionary<TKey, TValue>)
```csharp
protected void PostProcessEntities(World world, Dictionary<TKey, TValue> instancesToEntities)
```

This makes any fancy post process once all entities were created in the world.
            This may trigger reactive components within the world.

**Parameters** \
`world` [World](../../Bang/World.html) \
\
`instancesToEntities` [Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
\

#### AddFilter(string)
```csharp
public bool AddFilter(string name)
```

Add a new filter to group entities.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AddGroup(string)
```csharp
public bool AddGroup(string name)
```

Add a new folder to group entities.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### BelongsToAnyGroup(Guid)
```csharp
public bool BelongsToAnyGroup(Guid entity)
```

Checks whether an entity belongs to any group.

**Parameters** \
`entity` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DeleteFilter(string)
```csharp
public bool DeleteFilter(string name)
```

Delete a new filter to group entities.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DeleteGroup(string)
```csharp
public bool DeleteGroup(string name)
```

Delete a new folder to group entities.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasGroup(string)
```csharp
public bool HasGroup(string name)
```

Returns true if a folder group with the given name already exists in this world.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsOnFilter(Guid)
```csharp
public bool IsOnFilter(Guid g)
```

Returns true if the entity with the given GUID is in any active filter.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### MoveToGroup(string, Guid, int)
```csharp
public bool MoveToGroup(string targetGroup, Guid instance, int targetPosition)
```

Moves an entity instance to the specified folder group at the given position.

**Parameters** \
`targetGroup` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`targetPosition` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

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
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### FetchFolderNames()
```csharp
public IEnumerable<T> FetchFolderNames()
```

This is for editor purposes, return all the available folder names as an[IEnumerable<T>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0)

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### FetchAllSystems()
```csharp
public ImmutableArray<T> FetchAllSystems()
```

Returns all systems for this world, expanding nested feature assets recursively.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FetchEntitiesGuidInFilter(string)
```csharp
public ImmutableArray<T> FetchEntitiesGuidInFilter(string targetFilter)
```

Returns the GUIDs of all entities assigned to the specified filter.

**Parameters** \
`targetFilter` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FetchEntitiesOfGroup(string)
```csharp
public ImmutableArray<T> FetchEntitiesOfGroup(string name)
```

Returns the GUIDs of all entities assigned to the specified folder group.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FetchFilters()
```csharp
public ImmutableDictionary<TKey, TValue> FetchFilters()
```

This is for editor purposes, we group all entities in "folders" when visualizing them.
            This has no effect in the actual game.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### FetchFolders()
```csharp
public ImmutableDictionary<TKey, TValue> FetchFolders()
```

This is for editor purposes, we group all entities in "folders" when visualizing them.
            This has no effect in the actual game.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### GroupsCount()
```csharp
public int GroupsCount()
```

Returns the total number of folder groups defined in this world.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AssetsToBeSaved()
```csharp
public List<T> AssetsToBeSaved()
```

Returns and clears the list of dependent assets queued to be saved alongside this asset.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### FetchEntitiesInFilter(string)
```csharp
public List<T> FetchEntitiesInFilter(string targetFilter)
```

Returns the `EntityInstance` objects of all entities assigned to the specified filter.

**Parameters** \
`targetFilter` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### CreateInstance(Camera2D, ImmutableArray<T>)
```csharp
public MonoWorld CreateInstance(Camera2D camera, ImmutableArray<T> startingSystems)
```

Instantiates a new `MonoWorld` from this asset with the given camera and supplementary startup systems.

**Parameters** \
`camera` [Camera2D](../../Murder/Core/Graphics/Camera2D.html) \
`startingSystems` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[MonoWorld](../../Murder/Core/MonoWorld.html) \

#### CreateInstanceFromSave(SavedWorld, Camera2D, ImmutableArray<T>)
```csharp
public MonoWorld CreateInstanceFromSave(SavedWorld savedInstance, Camera2D camera, ImmutableArray<T> startingSystems)
```

Instantiates a `MonoWorld` from this asset, restoring entity state from the given `SavedWorld` snapshot.

**Parameters** \
`savedInstance` [SavedWorld](../../Murder/Assets/SavedWorld.html) \
`camera` [Camera2D](../../Murder/Core/Graphics/Camera2D.html) \
`startingSystems` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[MonoWorld](../../Murder/Core/MonoWorld.html) \

#### GetGroupOf(Guid)
```csharp
public string GetGroupOf(Guid entity)
```

Returns the group that an entity belongs.

**Parameters** \
`entity` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

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

#### TryGetInstance(Guid)
```csharp
public virtual EntityInstance TryGetInstance(Guid instanceGuid)
```

Retrieves the `EntityInstance` with the given GUID from this world; returns null if not found.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AfterDeserialized()
```csharp
public virtual void AfterDeserialized()
```

Called after deserialization; rebuilds internal entity instance caches.

#### AddInstance(EntityInstance)
```csharp
public void AddInstance(EntityInstance e)
```

Adds a new entity instance to this world.

**Parameters** \
`e` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### MakeGuid()
```csharp
public void MakeGuid()
```

Generates and assigns a new GUID to this asset.

#### MoveToFilter(string, Guid, int)
```csharp
public void MoveToFilter(string targetFilter, Guid instance, int targetPosition)
```

Moves an entity instance into the specified filter at the given position.

**Parameters** \
`targetFilter` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`targetPosition` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RemoveInstance(Guid)
```csharp
public void RemoveInstance(Guid instanceGuid)
```

Removes the entity instance with the given GUID from this world.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### TrackAssetOnSave(Guid)
```csharp
public void TrackAssetOnSave(Guid g)
```

Queues a dependent asset by GUID to be saved whenever this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### UpdateFeatures(ImmutableArray<T>)
```csharp
public void UpdateFeatures(ImmutableArray<T> features)
```

Replaces the world's feature list with the provided array.

**Parameters** \
`features` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### UpdateSystems(ImmutableArray<T>)
```csharp
public void UpdateSystems(ImmutableArray<T> systems)
```

Replaces the world's direct system list with the provided array.

**Parameters** \
`systems` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### ValidateInstances()
```csharp
public void ValidateInstances()
```

Validate instances are remove any entities that no longer exist in the asset.



⚡
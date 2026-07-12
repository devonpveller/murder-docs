# SaveData

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class SaveData : GameAsset
```

Tracks a saved game with all the player status.

**Intent:** Persist the entire runtime game state for one save slot: the current world, blackboard variable values, world-persistent entity deletions, and all active dynamic assets.

**Use-case:** Subclass `SaveData` to add game-specific save fields. Call `TryLoadLevel` to obtain a `SavedWorld` snapshot for a given world GUID, use `RecordRemovedEntityFromWorld` to mark persistent entity removals, and access `BlackboardTracker` to read and write global or character-scoped dialogue variables.

**Implements:** _[GameAsset](../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors

```csharp
protected SaveData(int saveSlot, float saveVersion, BlackboardTracker blackboardTracker)
```

**Parameters** \
`saveSlot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`saveVersion` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`blackboardTracker` [BlackboardTracker](../../Murder/Save/BlackboardTracker.html) \

```csharp
public SaveData(int saveSlot, float saveVersion)
```

**Parameters** \
`saveSlot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`saveVersion` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### \_entitiesOnWorldToDestroy

```csharp
protected readonly Dictionary<TKey, TValue> _entitiesOnWorldToDestroy;
```

List of all consumed entities throughout the map.
Mapped according to:
[World guid -&gt; [Entity Guid]]

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### BlackboardTracker

```csharp
public readonly BlackboardTracker BlackboardTracker;
```

Tracks all blackboard variables (global and character-scoped) for this save, used by the dialogue system.

**Returns** \
[BlackboardTracker](../../Murder/Save/BlackboardTracker.html) \

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

#### CurrentWorld

```csharp
public T? CurrentWorld { get; }
```

The GUID of the world that was active when this save was last written.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

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

#### IsSavePacked

```csharp
public virtual bool IsSavePacked { get; }
```

Whether this file will be packed in the save, if `IsStoredInSaveData` is true. Overridden to `true` on `SaveData`, since the save itself is what gets written into the slot's `saved.gz` (via `PackedSaveData`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path. Overridden to `true` on `SaveData`, since instances live under the save slot's own directory rather than the generic asset database.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; public set; }
```

Display name of this asset as shown in the editor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PendingOperation

```csharp
public Task? PendingOperation { get; }
```

The async task representing an in-progress `SaveAsync` world-snapshot operation, or null if none is running. Poll `HasFinishedSaveWorld` rather than inspecting this directly to know when it is safe to proceed (e.g. before quitting or switching maps).

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### Rename

```csharp
public bool Rename { get; public set; }
```

Whether the file should be renamed and the previous name deleted on next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SaveDataRelativeDirectoryPath

```csharp
public string SaveDataRelativeDirectoryPath { get; private set; }
```

This is save path, used by its assets.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SavedWorlds

```csharp
public ImmutableDictionary<TKey, TValue> SavedWorlds { get; private set; }
```

This maps
[World Guid -&gt; Saved World Guid]
that does not belong to a run and should be persisted.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### SaveLocation

```csharp
public virtual string SaveLocation { get; }
```

The folder path where this asset is saved on disk.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SaveName

```csharp
public string SaveName { get; private set; }
```

This is the name used in-game, specified by the user.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SaveRelativeDirectoryPath

```csharp
public string SaveRelativeDirectoryPath { get; private set; }
```

This is save path, used by its assets.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SaveSlot

```csharp
public readonly int SaveSlot;
```

Which save slot this belongs to. Default is zero.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SaveVersion

```csharp
public readonly float SaveVersion;
```

Game version, used for game save compatibility.

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

### ⭐ Methods

#### GetOrCreateEntitiesToBeDestroyedAt(World)

```csharp
protected HashSet<T> GetOrCreateEntitiesToBeDestroyedAt(World world)
```

Fetch the collected items at <paramref name="world" />.
If none, creates a new empty collection and returns that instead.

**Parameters** \
`world` [World](../../Bang/World.html) \

**Returns** \
[HashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) \

#### EntityToGuid(World, Entity)

```csharp
protected T? EntityToGuid(World world, Entity e)
```

Attempts to resolve the GUID of a live entity in the given world; returns null if the entity has no GUID.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### EntityToGuid(World, int)

```csharp
protected T? EntityToGuid(World world, int id)
```

Attempts to resolve the GUID of the entity with the given integer ID in the world; returns null if not found.

**Parameters** \
`world` [World](../../Bang/World.html) \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### GetDefaultSaveName()

```csharp
protected virtual string GetDefaultSaveName()
```

Returns the default display name for this save slot; override to customise the auto-generated name.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ClearAllWorlds()

```csharp
protected virtual void ClearAllWorlds()
```

This will clean all saved worlds.

#### OnModified()

```csharp
protected virtual void OnModified()
```

Called by the editor when the asset is modified; override to clear cached derived data.

#### HasFinishedSaveWorld()

```csharp
public bool HasFinishedSaveWorld()
```

Returns true when any pending asynchronous world-save operation has completed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RecordRemovedEntityFromWorld(World, Entity)

```csharp
public bool RecordRemovedEntityFromWorld(World world, Entity entity)
```

This records that an entity has been removed from the map.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entity` [Entity](../../Bang/Entities/Entity.html) \

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

#### TryLoadLevel(Guid)

```csharp
public virtual SavedWorld? TryLoadLevel(Guid guid)
```

Looks up the `SavedWorld` snapshot previously persisted for the world with GUID `guid` (via `SavedWorlds`), returning null if no snapshot exists for it yet. Call this when re-entering a world to check whether a saved layout should be restored instead of instantiating the `WorldAsset` from scratch.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[SavedWorld](../../Murder/Assets/SavedWorld.html) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Called after deserialization; override to rebuild caches from deserialized data.

#### ChangeSaveName(string)

```csharp
public void ChangeSaveName(string name)
```

Sets the player-facing display name of this save slot.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Initialize()

```csharp
public void Initialize()
```

Called after creating a fresh new save from this.

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new GUID to this asset.

#### OnBeforeMapSwitch(Guid)

```csharp
public virtual void OnBeforeMapSwitch(Guid nextWorld)
```

Called by the engine right before the active map is switched to `nextWorld`. Does nothing by default; override in a game-specific `SaveData` subclass to run custom logic (e.g. snapshotting extra state) prior to leaving the current world.

**Parameters** \
`nextWorld` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### OnBeforeSave(string)

```csharp
public virtual void OnBeforeSave(string? overridePath)
```

Called by the save system right before this `SaveData` is serialized to disk. Does nothing by default; override in a game-specific subclass to run custom logic (e.g. validation or derived-state recomputation) prior to persisting the save. `overridePath`, when non-null, is the alternate location the save is being written to instead of the default save directory.

**Parameters** \
`overridePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SaveAsync(MonoWorld)

```csharp
public void SaveAsync(MonoWorld world)
```

This saves a world that should be persisted across several runs.
For now, this will be restricted to the city.

**Parameters** \
`world` [MonoWorld](../../Murder/Core/MonoWorld.html) \

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Queues a dependent asset by GUID to be saved whenever this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### TrackCurrentWorld(Guid)

```csharp
public void TrackCurrentWorld(Guid guid)
```

Records the GUID of the world that is currently loaded, updating `CurrentWorld`.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

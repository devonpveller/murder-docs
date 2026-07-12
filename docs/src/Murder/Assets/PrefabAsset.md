# PrefabAsset

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class PrefabAsset : GameAsset, IEntity
```

A reusable entity template that can be instantiated multiple times in a world or used as a child of another prefab.

**Intent:** Define a self-contained, editor-authored entity layout (components + children) that can be stamped into any world by reference, enabling consistent reuse of complex entity setups.

**Use-case:** Create a `PrefabAsset` for repeated game objects (crates, NPCs, traps). Place it in levels via the editor, or call `CreateAndFetch` at runtime to spawn a live entity. Use `ToInstance` to create an `EntityInstance` from the prefab for placement in a `WorldAsset`.

**Implements:** _[GameAsset](../../Murder/Assets/GameAsset.html), [IEntity](../../Murder/Prefabs/IEntity.html)_

### ⭐ Constructors

```csharp
public PrefabAsset()
```

```csharp
public PrefabAsset(EntityInstance instance)
```

**Parameters** \
`instance` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

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

#### Children

```csharp
public ImmutableArray<T> Children { get; }
```

GUIDs of the child `EntityInstance` objects nested beneath this prefab's root entity. Use `FetchChildren` to resolve the actual `EntityInstance` objects, or `TryGetChild` to look one up by GUID.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Components

```csharp
public ImmutableArray<T> Components { get; }
```

Ordered list of ECS components attached to the root entity of this prefab.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Dimensions

```csharp
public readonly TileDimensions Dimensions;
```

Dimensions of the prefab. Used when drawing it on the map or the editor.

**Returns** \
[TileDimensions](../../Murder/Core/TileDimensions.html) \

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

#### PrefabRefName

```csharp
public string? PrefabRefName { get; }
```

Forwards to the underlying root `EntityInstance`'s `PrefabRefName`; non-null only when this asset was built on top of another prefab reference (see `PrefabEntityInstance`), in which case it names that base prefab.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

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

#### ShowOnPrefabSelector

```csharp
public bool ShowOnPrefabSelector;
```

Whether this should show in the editor selector.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

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

Called by the editor when the asset is modified; override to clear cached derived data.

#### HasComponent(IComponent)

```csharp
public bool HasComponent(IComponent c)
```

Returns true if the root entity of this prefab has a component matching the type of `c`.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CreateAndFetch(World)

```csharp
public Entity CreateAndFetch(World world)
```

Spawns this prefab into the given world and returns the resulting `Entity`.

**Parameters** \
`world` [World](../../Bang/World.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### ToInstance(string)

```csharp
public EntityInstance ToInstance(string name)
```

Creates a new instance entity from the current asset.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

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

#### ToInstanceAsAsset(string)

```csharp
public PrefabAsset ToInstanceAsAsset(string name)
```

Creates a new `PrefabAsset` whose root entity data is derived from this prefab, using the given display name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[PrefabAsset](../../Murder/Assets/PrefabAsset.html) \

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

#### AddOrReplaceComponentForChild(Guid, IComponent)

```csharp
public bool AddOrReplaceComponentForChild(Guid childGuid, IComponent component)
```

Adds or replaces the specified component on the child entity identified by `childGuid`.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`component` [IComponent](../../Bang/Components/IComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanRemoveChild(Guid)

```csharp
public bool CanRemoveChild(Guid instanceGuid)
```

Returns true if the child entity with the given GUID can be safely removed from this prefab.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanRevertComponent(Type)

```csharp
public bool CanRevertComponent(Type t)
```

Returns true if the component of type `t` has been overridden and can be reverted to its prefab-default value.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponent(Type)

```csharp
public bool HasComponent(Type type)
```

Returns true if the root entity of this prefab has a component of the specified type.

**Parameters** \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponentAtChild(Guid, Type)

```csharp
public bool HasComponentAtChild(Guid childGuid, Type type)
```

Returns true if the child entity with the given GUID has a component of the specified type.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveChild(Guid)

```csharp
public bool RemoveChild(Guid instanceGuid)
```

Removes the child `EntityInstance` identified by `instanceGuid` from this prefab's root entity; returns true if a child with that GUID was found and removed.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveComponent(Type)

```csharp
public bool RemoveComponent(Type t)
```

Removes the component of type `t` from the root entity of this prefab; returns true if it was present.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RevertComponent(Type)

```csharp
public virtual bool RevertComponent(Type t)
```

Reverts a component override of type `t` on the root entity back to its inherited prefab default.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RevertComponentForChild(Guid, Type)

```csharp
public bool RevertComponentForChild(Guid childGuid, Type t)
```

Reverts a component override of type `t` on the specified child entity back to its inherited default.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetChild(Guid, out EntityInstance&)

```csharp
public bool TryGetChild(Guid guid, EntityInstance& instance)
```

Attempts to retrieve the child `EntityInstance` with the given GUID; returns false if not found.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`instance` [EntityInstance&](../../Murder/Prefabs/EntityInstance.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetComponent(Type)

```csharp
public IComponent GetComponent(Type type)
```

Retrieves the component of the specified type from the root entity of this prefab.

**Parameters** \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \

#### TryGetComponentForChild(Guid, Type)

```csharp
public IComponent? TryGetComponentForChild(Guid guid, Type t)
```

Attempts to retrieve the component of type `t` from the specified child entity; returns null if absent.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \

#### FetchChildren()

```csharp
public ImmutableArray<T> FetchChildren()
```

Returns all child `EntityInstance` objects nested within this prefab.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetChildComponents(Guid)

```csharp
public ImmutableArray<T> GetChildComponents(Guid childGuid)
```

Returns all components attached to the child entity with the given GUID.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Create(World, Entity?)

```csharp
public int Create(World world, Entity? replaceEntity = null)
```

Create an instance of the entity and all of its children. When `replaceEntity` is provided, the new components are merged into that existing entity instead of creating a brand-new one (used internally by `Replace`).

**Parameters** \
`world` [World](../../Bang/World.html) \
`replaceEntity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AddChild(EntityInstance)

```csharp
public void AddChild(EntityInstance asset)
```

Adds the given `EntityInstance` as a nested child of this prefab's root entity.

**Parameters** \
`asset` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AddOrReplaceComponent(IComponent)

```csharp
public void AddOrReplaceComponent(IComponent c)
```

Adds or replaces a component on the root entity of this prefab.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Called after deserialization; override to rebuild caches from deserialized data.

#### RemoveComponentForChild(Guid, Type)

```csharp
public void RemoveComponentForChild(Guid childGuid, Type t)
```

Removes the component of type `t` from the specified child entity.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new GUID to this asset.

#### Replace(World, Entity, IComponent[])

```csharp
public void Replace(World world, Entity e, IComponent[] startWithComponents)
```

This will replace an existing entity in the world.
It keeps some elements of the original entity: position and target id components.

**Parameters** \
`world` [World](../../Bang/World.html) \
\
`e` [Entity](../../Bang/Entities/Entity.html) \
\
`startWithComponents` [IComponent[]](../../Bang/Components/IComponent.html) \
\

#### Replace(World, Entity)

```csharp
public void Replace(World world, Entity e)
```

This will replace an existing entity in the world.
It keeps some elements of the original entity: position and target id components.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Queues a dependent asset by GUID to be saved whenever this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

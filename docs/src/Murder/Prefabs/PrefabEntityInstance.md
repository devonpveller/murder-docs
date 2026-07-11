# PrefabEntityInstance

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public class PrefabEntityInstance : EntityInstance, IEntity
```

An `EntityInstance` that is bound to a `PrefabAsset` and can store per-instance overrides for components and children via `EntityModifier` records.

**Intent:** Represents a placed prefab reference in a world or parent entity, tracking which components or children differ from the base prefab definition.

**Use-case:** Used by the editor when placing prefab entities in a scene; at runtime the engine uses the modifier data to construct the final entity with both base prefab components and instance-specific overrides.

**Implements:** _[EntityInstance](../../Murder/Prefabs/EntityInstance.html), [IEntity](../../Murder/Prefabs/IEntity.html)_

### ⭐ Constructors
```csharp
public PrefabEntityInstance()
```
Creates a new empty prefab entity instance.

### ⭐ Properties
#### _children
```csharp
protected Dictionary<TKey, TValue> _children;
```
Mutable map from child GUID to child `EntityInstance` definitions.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### _components
```csharp
protected readonly Dictionary<TKey, TValue> _components;
```
List of custom component values that differ from the parent prefab's defaults.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### ActivateWithParent
```csharp
public bool ActivateWithParent;
```
When `true`, this instance's activation state is propagated from the parent entity.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Children
```csharp
public virtual ImmutableArray<T> Children { get; }
```
Immutable list of child entity identifiers merged from the base prefab and any instance additions.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Components
```csharp
public virtual ImmutableArray<T> Components { get; }
```

Returns all the components of the entity asset, followed by all the components of the instance.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Guid
```csharp
public virtual Guid Guid { get; }
```
Unique identifier for this entity instance.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Id
```csharp
public T? Id;
```
Optional world-level entity ID preserved across save files.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### IsDeactivated
```csharp
public bool IsDeactivated;
```
When `true`, this entity starts deactivated when placed in the world.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsEmpty
```csharp
public virtual bool IsEmpty { get; }
```
Returns `true` if this instance has no component overrides and no added children.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Name
```csharp
public virtual string Name { get; }
```
Display name of this entity instance.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### PrefabRef
```csharp
public readonly PrefabReference PrefabRef;
```

This is the guid of the [PrefabAsset](../../Murder/Assets/PrefabAsset.html) that this refers to.

**Returns** \
[PrefabReference](../../Murder/Prefabs/PrefabReference.html) \
#### PrefabRefName
```csharp
public virtual string PrefabRefName { get; }
```
Name of the underlying `PrefabAsset`, or `null` if this is a standalone instance.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### CanRevertComponentForChild(Guid, Type)
```csharp
public bool CanRevertComponentForChild(Guid guid, Type t)
```
Returns `true` if the component of type `t` on the child identified by `guid` can be reverted to its base prefab value.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FetchChildChildren(IEntity)
```csharp
public ImmutableArray<T> FetchChildChildren(IEntity child)
```

Get all the children of a child.
            This will take into account any modifiers of the parent.

**Parameters** \
`child` [IEntity](../../Murder/Prefabs/IEntity.html) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### CreateChildrenlessInstance(Guid)
```csharp
public PrefabEntityInstance CreateChildrenlessInstance(Guid assetGuid)
```
Creates a copy of this instance linked to `assetGuid` but with no children, used for lightweight prefab references.

**Parameters** \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[PrefabEntityInstance](../../Murder/Prefabs/PrefabEntityInstance.html) \

#### AddOrReplaceComponentForChild(Guid, IComponent)
```csharp
public virtual bool AddOrReplaceComponentForChild(Guid instance, IComponent component)
```
Adds or replaces `component` on the child identified by `instance`; returns `true` if the child was found.

**Parameters** \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`component` [IComponent](../../Bang/Components/IComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanModifyChildAt(Guid)
```csharp
public virtual bool CanModifyChildAt(Guid childId)
```

This checks whether a child can be modified.
            This means that it does not belong to any prefab reference.

**Parameters** \
`childId` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanRemoveChild(Guid)
```csharp
public virtual bool CanRemoveChild(Guid instanceGuid)
```
Returns `true` if the child with the given GUID can be removed from this prefab instance.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanRevertComponent(Type)
```csharp
public virtual bool CanRevertComponent(Type t)
```
Returns `true` if the component of the given type can be reverted to the base prefab value.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponent(Type)
```csharp
public virtual bool HasComponent(Type type)
```

Returns whether an instance of <paramref name="type" /> exists in the list of components.

**Parameters** \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponentAtChild(Guid, Type)
```csharp
public virtual bool HasComponentAtChild(Guid instance, Type type)
```
Returns `true` if the child identified by `instance` has a component of the given type.

**Parameters** \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsComponentInAsset(IComponent)
```csharp
public virtual bool IsComponentInAsset(IComponent c)
```

Returns whether a component is present in the entity asset.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveAllComponents()
```csharp
public virtual bool RemoveAllComponents()
```
Removes all component overrides from this instance; returns `true` if any were removed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveChild(Guid)
```csharp
public virtual bool RemoveChild(Guid instanceGuid)
```
Removes the child entity with the given GUID; returns `true` if it was found.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveComponent(Type)
```csharp
public virtual bool RemoveComponent(Type t)
```
Removes the component override of the given type; returns `true` if it was present.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RevertComponent(Type)
```csharp
public virtual bool RevertComponent(Type t)
```
Reverts the component of the given type to the base prefab value; returns `true` if the revert succeeded.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RevertComponentForChild(Guid, Type)
```csharp
public virtual bool RevertComponentForChild(Guid childGuid, Type t)
```
Reverts the component of type `t` on the child identified by `childGuid`; returns `true` if reverted.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetChild(Guid, out EntityInstance&)
```csharp
public virtual bool TryGetChild(Guid guid, EntityInstance& instance)
```
Attempts to find the child with the given GUID; returns `true` and populates `instance` if found.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`instance` [EntityInstance&](../../Murder/Prefabs/EntityInstance.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetChild(Guid)
```csharp
public virtual EntityInstance GetChild(Guid instanceGuid)
```
Returns the child entity instance with the given GUID; throws if not found.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### GetComponent(Type)
```csharp
public virtual IComponent GetComponent(Type componentType)
```
Returns the component of the given type; throws if not present.

**Parameters** \
`componentType` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \

#### TryGetComponentForChild(Guid, Type)
```csharp
public virtual IComponent TryGetComponentForChild(Guid guid, Type t)
```
Returns the component of type `t` from the child with GUID `guid`, or `null` if not present.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \

#### FetchChildren()
```csharp
public virtual ImmutableArray<T> FetchChildren()
```

Returns all the children of the entity asset, followed by all the children of the instance.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetChildComponents(Guid)
```csharp
public virtual ImmutableArray<T> GetChildComponents(Guid guid)
```

Fetch the components for a given child.
            This will filter any modifiers made to the children components.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Create(World, IEntity)
```csharp
public virtual int Create(World world, IEntity parent)
```

**Parameters** \
`world` [World](../../Bang/World.html) \
`parent` [IEntity](../../Murder/Prefabs/IEntity.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Create(World)
```csharp
public virtual int Create(World world)
```

Create the instance entity in the world.

**Parameters** \
`world` [World](../../Bang/World.html) \
\

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AddChild(EntityInstance)
```csharp
public virtual void AddChild(EntityInstance asset)
```
Adds `asset` as a child of this prefab entity instance.

**Parameters** \
`asset` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AddChildAtChild(Guid, EntityInstance)
```csharp
public virtual void AddChildAtChild(Guid childId, EntityInstance instance)
```
Adds `instance` as a grandchild under the child identified by `childId`.

**Parameters** \
`childId` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`instance` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AddOrReplaceComponent(IComponent)
```csharp
public virtual void AddOrReplaceComponent(IComponent c)
```
Adds or replaces component `c` as a per-instance override.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \

#### RemoveChildAtChild(Guid, Guid)
```csharp
public virtual void RemoveChildAtChild(Guid childId, Guid instance)
```
Removes the grandchild identified by `instance` from the child identified by `childId`.

**Parameters** \
`childId` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RemoveComponentForChild(Guid, Type)
```csharp
public virtual void RemoveComponentForChild(Guid instance, Type t)
```
Removes the component of type `t` from the child identified by `instance`.

**Parameters** \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### SetName(string)
```csharp
public virtual void SetName(string name)
```
Sets the display name of this entity instance.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### UpdateGuid(Guid)
```csharp
public void UpdateGuid(Guid newGuid)
```
Replaces the GUID of this entity instance with `newGuid`.

**Parameters** \
`newGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \



⚡
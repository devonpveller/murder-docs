# EntityInstance

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public class EntityInstance : IEntity
```

Represents an entity as an instance placed on the map.
            This map may be relative to the world or another entity.

**Intent:** Records a single entity placement inside a prefab or world asset, including its component data and GUID.

**Use-case:** Used by the editor and runtime to represent positioned entities in a world or nested inside a prefab; instantiate via `PrefabAsset.CreateInstance`.

**Implements:** _[IEntity](../../Murder/Prefabs/IEntity.html)_

### ⭐ Constructors
```csharp
public EntityInstance()
```

```csharp
public EntityInstance(string name, Guid guid)
```
Creates a new entity instance with the given display name and GUID.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public EntityInstance(string name, T? guid)
```
Creates a new entity instance with the given display name and optional GUID.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`guid` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

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

List of custom components that difer from the parent entity.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### ActivateWithParent
```csharp
public bool ActivateWithParent;
```

Whether this instance must have its activation propagated according to the parent. 
            <br /><br />
            TODO: We might need to revisit on whether this is okay/actually scales well.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Children
```csharp
public virtual ImmutableArray<T> Children { get; }
```
Immutable list of child `EntityInstance` identifiers for this entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Components
```csharp
public virtual ImmutableArray<T> Components { get; }
```
Immutable list of all components attached to this entity instance.

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

Entity id, if any. This will be persisted across save files.
            This only exists for instances in the world.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### IsDeactivated
```csharp
public bool IsDeactivated;
```

Returns whether the entity is currently deactivated once instantiated in the map.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsEmpty
```csharp
public virtual bool IsEmpty { get; }
```
Returns `true` if this instance has no components and no children.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Name
```csharp
public virtual string Name { get; }
```
Display name of this entity instance.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### PrefabRefName
```csharp
public virtual string PrefabRefName { get; }
```

By default, this is not based on any prefab.
            Return null.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### AddOrReplaceComponentForChild(Guid, IComponent)
```csharp
public virtual bool AddOrReplaceComponentForChild(Guid childGuid, IComponent component)
```
Adds or replaces `component` on the child identified by `childGuid`; returns `true` if the child was found.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`component` [IComponent](../../Bang/Components/IComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanRemoveChild(Guid)
```csharp
public virtual bool CanRemoveChild(Guid instanceGuid)
```
Returns `true` if the child with the given GUID can be removed from this instance.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanRevertComponent(Type)
```csharp
public virtual bool CanRevertComponent(Type t)
```
Returns `true` if the component of the given type can be reverted to its base value.

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
public virtual bool HasComponentAtChild(Guid childGuid, Type type)
```
Returns `true` if the child identified by `childGuid` has a component of the given type.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
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
Removes all components from this entity instance; returns `true` if any were removed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveChild(Guid)
```csharp
public virtual bool RemoveChild(Guid instanceGuid)
```
Removes the child entity with the given GUID from this instance; returns `true` if it was found and removed.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveComponent(Type)
```csharp
public virtual bool RemoveComponent(Type t)
```
Removes the component of the given type from this instance; returns `true` if it was present.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RevertComponent(Type)
```csharp
public virtual bool RevertComponent(Type t)
```
Reverts the component of the given type to its base value; returns `true` if the revert succeeded.

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
Returns all child `EntityInstance` objects as an immutable array.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetChildComponents(Guid)
```csharp
public virtual ImmutableArray<T> GetChildComponents(Guid guid)
```

Try to get the components for a child.
            TODO: Do not expose the instance children directly...? Is this only necessary for prefabs?
            Are we limiting the amount of children recursive to two?

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
\

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Create(World, IEntity)
```csharp
public virtual int Create(World world, IEntity parent)
```

Create the instance entity in the world with a specified parent.

**Parameters** \
`world` [World](../../Bang/World.html) \
\
`parent` [IEntity](../../Murder/Prefabs/IEntity.html) \
\

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
Adds `asset` as a child of this entity instance.

**Parameters** \
`asset` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AddOrReplaceComponent(IComponent)
```csharp
public virtual void AddOrReplaceComponent(IComponent c)
```
Adds or replaces component `c` on this entity instance.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \

#### RemoveComponentForChild(Guid, Type)
```csharp
public virtual void RemoveComponentForChild(Guid childGuid, Type t)
```
Removes the component of type `t` from the child identified by `childGuid`.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### SetName(string)
```csharp
public virtual void SetName(string name)
```

Set the name of the entity instance.

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
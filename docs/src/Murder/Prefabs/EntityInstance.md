# EntityInstance

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public class EntityInstance : IEntity
```

Represents an entity as an instance placed on the map.
This map may be relative to the world or another entity.

**Intent:** Records a single entity placement inside a prefab or world asset — its display name, GUID, component overrides and children — as serializable data, independent of any `World`. This is the format world/prefab asset files are saved as; `Create` is what turns it into an actual live `Entity`.

**Use-case:** Used by the level/prefab editor to represent entities being authored, and by `WorldAsset`/`PrefabAsset` to store their entity trees on disk. Build one with `EntityBuilder.CreateInstance`, `PrefabAsset.ToInstance`, or one of this type's own constructors, then call `Create(World, ...)` to spawn it. `PrefabEntityInstance` extends this to additionally track a link back to a `PrefabAsset` and the per-child overrides applied on top of it.

**Implements:** _[IEntity](../../Murder/Prefabs/IEntity.html)_

### ⭐ Constructors

```csharp
public EntityInstance()
```

Parameterless constructor required for deserialization; produces an entity instance with an empty name and a freshly generated `Guid`. Prefer `EntityBuilder.CreateInstance` or one of the other constructors when creating instances from code.

```csharp
public EntityInstance(string name, Guid guid)
```

The canonical constructor, marked `[JsonConstructor]` so the serializer uses it when deserializing an instance from a world/prefab asset file. Sets both the display `name` and the identity `guid` explicitly; use this when you need full control over both (for example, when restoring a previously-saved instance and want to preserve its exact GUID).

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public EntityInstance(string? name, Guid? guid = null)
```

Convenience constructor used by most call sites: creates a new entity instance with the given display name, defaulting `name` to an empty string when omitted and generating a new random `Guid` when `guid` is not provided. This delegates to the `(string name, Guid guid)` constructor above.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`guid` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

### ⭐ Properties

#### \_children

```csharp
protected Dictionary<TKey, TValue> _children;
```

Mutable map from child GUID to child `EntityInstance` definitions.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### \_components

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
public Guid Guid { get; }
```

Unique identifier for this entity instance, backed by the private `_guid` field. This is not `virtual` — `PrefabEntityInstance` and every other implementer share the same storage and identity semantics, so there is nothing to override. Used throughout the prefab system (as the key in `EntityModifier` maps, `_children` dictionaries, etc.) to refer to a specific instance without holding a reference to the object itself.

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

Returns `true` if this instance has no non-`IntrinsicAttribute` components and no children — i.e. it would spawn a functionally empty entity. Intrinsic components (like transform/position) don't count, since virtually every entity has one by default. `PrefabEntityInstance` overrides this to also treat a resolvable prefab reference as non-empty.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; }
```

Display name of this entity instance, backed by the private `_name` field. Not `virtual` — use `SetName` to change it. This is what shows up in the editor's entity/hierarchy panel and is used by `PrefabAsset.GetSimplifiedName`-style helpers.

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

#### Create(World, Entity)

```csharp
public virtual int Create(World world, Entity? replaceEntity = null)
```

Creates this instance's entity (and, recursively, all of its children) inside `world`. This is the entry point most callers use — `PrefabAsset.Create`/`CreateAndFetch` simply forward to it. When `replaceEntity` is provided, the target entity is replaced in place (via `EntityBuilder.Replace`) instead of a brand-new one being added, preserving the existing entity's position and ID-target components; this is how a designer swapping a placed entity's prefab in the editor, or `PrefabAsset.Replace`, avoids having to re-wire references to the old entity ID.

**Parameters** \
`world` [World](../../Bang/World.html) \
`replaceEntity` [Entity](../../Bang/Entities/Entity.html) \

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
public void AddOrReplaceComponent(IComponent c)
```

Adds or replaces component `c` on this entity instance. Not `virtual` — every subtype shares the same underlying `_components` dictionary storage for its own instance-level overrides.

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
public void SetName(string name)
```

Set the name of the entity instance. Not `virtual` — this always writes directly to the private `_name` backing field, even on a `PrefabEntityInstance`, so it does not need any override-specific behavior.

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

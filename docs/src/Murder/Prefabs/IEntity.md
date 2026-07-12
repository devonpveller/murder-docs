# IEntity

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public abstract IEntity
```

Base contract for anything that can be placed in a world as an entity, whether a standalone `EntityInstance` or a `PrefabEntityInstance` tied to a prefab asset.

**Intent:** Provides a uniform API for reading and modifying entities and their children regardless of whether they are raw instances or prefab-backed instances, so editor/tooling code (and `PrefabAsset`, which also implements it) does not need to special-case which kind of entity data it is looking at.

**Use-case:** Used by the level/prefab editor (`Stage_Instances`, `SearchBox`, `CustomEditor`) to read/write entity data uniformly, and implemented by `EntityInstance`, `PrefabEntityInstance` and `PrefabAsset` itself. If you're writing editor tooling that needs to inspect or mutate "an entity that hasn't been spawned yet", code against this interface rather than against `EntityInstance` directly so it also works with prefab assets.

### ⭐ Properties

#### Children

```csharp
public abstract virtual ImmutableArray<T> Children { get; }
```

Returns all the identifiers for this entity children.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Components

```csharp
public abstract virtual ImmutableArray<T> Components { get; }
```

Returns all the components of the entity asset, followed by all the components of the instance.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Guid

```csharp
public abstract virtual Guid Guid { get; }
```

Unique identifier for this entity instance.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Name

```csharp
public abstract virtual string Name { get; }
```

Display name of this entity instance.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PrefabRefName

```csharp
public abstract virtual string PrefabRefName { get; }
```

If this has a prefab reference, this will return its name.
Otherwise, return null.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### AddOrReplaceComponentForChild(Guid, IComponent)

```csharp
public abstract bool AddOrReplaceComponentForChild(Guid childGuid, IComponent component)
```

Adds or replaces `component` on the child identified by `childGuid`; returns `true` if the child was found.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`component` [IComponent](../../Bang/Components/IComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanRemoveChild(Guid)

```csharp
public abstract bool CanRemoveChild(Guid instanceGuid)
```

Returns `true` if the child with the given GUID can be removed from this entity.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanRevertComponent(Type)

```csharp
public abstract bool CanRevertComponent(Type type)
```

Returns `true` if the component of the given type can be reverted to the base prefab value.

**Parameters** \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponent(Type)

```csharp
public abstract bool HasComponent(Type type)
```

Returns `true` if a component of the given type exists on this entity.

**Parameters** \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponentAtChild(Guid, Type)

```csharp
public abstract bool HasComponentAtChild(Guid childGuid, Type type)
```

Returns `true` if the child identified by `childGuid` has a component of the given type.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveChild(Guid)

```csharp
public abstract bool RemoveChild(Guid guid)
```

Removes the child entity identified by `guid` from this entity, if it can be removed (see `CanRemoveChild`). Returns `true` if it was found and removed.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveComponent(Type)

```csharp
public abstract bool RemoveComponent(Type t)
```

Removes the component of type `t` from this entity, if present. Returns `true` if it was found and removed.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RevertComponent(Type)

```csharp
public abstract bool RevertComponent(Type t)
```

Reverts the component of type `t` back to its base/prefab value, discarding any instance-level override. See `CanRevertComponent` to check first.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RevertComponentForChild(Guid, Type)

```csharp
public abstract bool RevertComponentForChild(Guid childGuid, Type t)
```

Reverts the component of type `t` on the child identified by `childGuid` to its base prefab value; returns `true` if reverted.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetChild(Guid, out EntityInstance&)

```csharp
public abstract bool TryGetChild(Guid guid, EntityInstance& instance)
```

Attempts to find the child entity with the given GUID; returns `true` and populates `instance` if found.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`instance` [EntityInstance&](../../Murder/Prefabs/EntityInstance.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetComponent(Type)

```csharp
public abstract IComponent GetComponent(Type componentType)
```

Returns the component of the given type on this entity; throws if not present.

**Parameters** \
`componentType` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \

#### TryGetComponentForChild(Guid, Type)

```csharp
public abstract IComponent TryGetComponentForChild(Guid guid, Type t)
```

Returns the component of type `t` from the child with GUID `guid`, or `null` if not present.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \

#### FetchChildren()

```csharp
public abstract ImmutableArray<T> FetchChildren()
```

**INTERNAL ONLY**
Fetches the actual entities for all children.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetChildComponents(Guid)

```csharp
public abstract ImmutableArray<T> GetChildComponents(Guid guid)
```

Returns all components of the child entity identified by `guid`.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Create(World, Entity)

```csharp
public abstract int Create(World world, Entity? replace = null)
```

Create the entity in the world! When `replace` is provided, the target entity is replaced in place instead of a new one being added. Both `EntityInstance` and `PrefabEntityInstance` implement this by delegating to `EntityBuilder.Create`/`Replace`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`replace` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AddChild(EntityInstance)

```csharp
public abstract void AddChild(EntityInstance asset)
```

Adds `asset` as a child entity of this instance.

**Parameters** \
`asset` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AddOrReplaceComponent(IComponent)

```csharp
public abstract void AddOrReplaceComponent(IComponent c)
```

Adds or replaces component `c` on this entity.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \

#### RemoveComponentForChild(Guid, Type)

```csharp
public abstract void RemoveComponentForChild(Guid childGuid, Type t)
```

Removes the component of type `t` from the child identified by `childGuid`.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### SetName(string)

```csharp
public abstract void SetName(string name)
```

Sets the display name of this entity instance.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetComponent()

```csharp
public virtual T GetComponent()
```

Returns the component of type `T` on this entity; throws if not present.

**Returns** \
[T](../../) \

⚡

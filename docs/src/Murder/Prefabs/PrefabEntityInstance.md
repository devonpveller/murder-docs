# PrefabEntityInstance

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public class PrefabEntityInstance : EntityInstance, IEntity
```

An `EntityInstance` that is bound to a `PrefabAsset` via a `PrefabReference` and can store per-instance overrides for its own components/children as well as per-child overrides (via `EntityModifier`) for anything nested inside the prefab.

**Intent:** This is what a "prefab placed in the world" actually is at the data level. Rather than copying the prefab's components/children at placement time, it keeps a live reference (`PrefabRef`) to the source `PrefabAsset` and layers its own deltas on top: `_components`/`_removeComponent` for this entity's own overrides, and `_childrenModifiers` (a `Guid -> EntityModifier` map) for overrides applied to entities nested inside the prefab, however deep. `Components`, `Children`, `FetchChildren`, `GetComponent`, etc. are all overridden to merge the prefab's data with these deltas on the fly, so editing the source prefab later automatically propagates to every placed instance that hasn't explicitly overridden the changed part.

**Use-case:** Created whenever the level editor places a prefab into a world or into another prefab (`EntityBuilder.CreateInstance` returns one whenever `assetGuid != Guid.Empty`). Designers use the `*ForChild` and `*AtChild` methods to tweak a specific nested child without detaching it from the prefab, and `RevertComponent`/`RevertComponentForChild` to undo an override back to the prefab's value. At runtime, `Create`/`CreateInternal` resolve the full modifier chain (including modifiers inherited from the prefab's own `PrefabEntityInstance` children) and hand the result to `EntityBuilder` to actually spawn the entity.

**Implements:** _[EntityInstance](../../Murder/Prefabs/EntityInstance.html), [IEntity](../../Murder/Prefabs/IEntity.html)_

### ⭐ Constructors

```csharp
public PrefabEntityInstance()
```

Creates a new empty prefab entity instance.

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
public override ImmutableArray<T> Children { get; }
```

Immutable list of child entity identifiers, merged from the base prefab's children and this instance's own additions. When the instance was created via `CreateChildrenlessInstance` (`_ignorePrefabChildren == true`), the prefab's children are skipped entirely and only this instance's own additions are returned — used for lightweight references that don't need to duplicate the prefab's child tree.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Components

```csharp
public override ImmutableArray<T> Components { get; }
```

Returns the base prefab's components (via `PrefabRef.Fetch()`), with any type that this instance overrides or explicitly removed filtered out, followed by this instance's own override components. This is what `EntityBuilder` reads when spawning the entity, so the result always reflects the prefab's current data plus this instance's deltas.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Guid

```csharp
public Guid Guid { get; }
```

Unique identifier for this entity instance. Not `virtual`/overridden — inherited directly from `EntityInstance`, which backs it with a plain field.

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
public override bool IsEmpty { get; }
```

Returns `true` only when this instance's `PrefabRef` cannot be resolved (`CanFetch` is `false`) **and** the base `EntityInstance.IsEmpty` check also passes (no non-intrinsic component overrides and no added children). A `PrefabEntityInstance` bound to a real, resolvable prefab is therefore never considered empty, since it will always spawn at least the prefab's own entity.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; }
```

Display name of this entity instance. Not `virtual`/overridden — inherited directly from `EntityInstance`. Defaults to the prefab's simplified name when the instance is constructed without an explicit name.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PrefabRef

```csharp
public readonly PrefabReference PrefabRef;
```

The [PrefabReference](../../Murder/Prefabs/PrefabReference.html) (i.e. the guid) of the [PrefabAsset](../../Murder/Assets/PrefabAsset.html) that this instance is placed from. This is what every overridden member (`Components`, `Children`, `GetComponent`, etc.) resolves against to merge the prefab's base data with this instance's own overrides.

**Returns** \
[PrefabReference](../../Murder/Prefabs/PrefabReference.html) \

#### PrefabRefName

```csharp
public override string? PrefabRefName { get; }
```

Name of the underlying `PrefabAsset`, resolved via `PrefabRef.Fetch().GetSimplifiedName()`. Used by the editor to display which prefab a placed instance comes from.

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
public static PrefabEntityInstance CreateChildrenlessInstance(Guid assetGuid)
```

Static factory that creates a brand-new, unnamed `PrefabEntityInstance` bound to `assetGuid` with `_ignorePrefabChildren` set, so its `Children`/`FetchChildren` never pull in the prefab's own children — only ones explicitly added afterward. Used for lightweight prefab references where duplicating the whole nested child tree isn't wanted (e.g. referencing a prefab from another asset just to read its data or spawn it standalone).

**Parameters** \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[PrefabEntityInstance](../../Murder/Prefabs/PrefabEntityInstance.html) \

#### AddOrReplaceComponentForChild(Guid, IComponent)

```csharp
public override bool AddOrReplaceComponentForChild(Guid instance, IComponent component)
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
public override bool CanRemoveChild(Guid instanceGuid)
```

Returns `true` if the child with the given GUID can be removed from this prefab instance — specifically, `false` when the child belongs to the base prefab itself (only children added by this instance, or one of its `EntityModifier`s, can be removed).

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanRevertComponent(Type)

```csharp
public override bool CanRevertComponent(Type t)
```

Returns `true` if this instance currently overrides a component of type `t` (via `AddOrReplaceComponent`) **and** the base prefab also has a component of that type — i.e. there is a prefab value to revert back to.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponent(Type)

```csharp
public override bool HasComponent(Type type)
```

Returns `true` if either the base prefab (`PrefabRef.Fetch()`) or this instance's own overrides have a component of `type`. Note this does not account for `_removeComponent` — see `Components`/`GetComponent` for the effective, filtered view.

**Parameters** \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponentAtChild(Guid, Type)

```csharp
public override bool HasComponentAtChild(Guid instance, Type type)
```

Returns `true` if a component of the given `type` is present on the child, taking any `EntityModifier` for that child into account first: it checks whether the modifier explicitly removed the type (returns `false`), then whether the modifier overrides it (returns `true`), and finally falls back to the child's own components.

**Parameters** \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsComponentInAsset(IComponent)

```csharp
public override bool IsComponentInAsset(IComponent c)
```

Returns whether `c` is present in the base prefab (`PrefabRef.Fetch().HasComponent(c)`) — i.e. whether it comes from the prefab asset itself rather than being an instance-only addition. Used by the editor to decide whether a component should be shown as "revertable".

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
public override bool RemoveChild(Guid instanceGuid)
```

Removes the child entity with the given GUID. First tries this instance's own direct children (`base.RemoveChild`); if not found there, searches every `EntityModifier`'s added children and removes it from whichever one has it. Returns `true` if it was found and removed from either place.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveComponent(Type)

```csharp
public override bool RemoveComponent(Type t)
```

Removes any instance-level override for component type `t` (via the base implementation) and, if the base prefab itself has a component of that type that hasn't already been marked removed, additionally marks it as removed so it no longer appears in `Components`/`GetComponent`.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RevertComponent(Type)

```csharp
public override bool RevertComponent(Type t)
```

Discards this instance's override for component type `t` (equivalent to `base.RemoveComponent(t)`, which does **not** mark it as removed), letting the base prefab's value show through again. Pair with `CanRevertComponent` to know when this is meaningful.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RevertComponentForChild(Guid, Type)

```csharp
public override bool RevertComponentForChild(Guid childGuid, Type t)
```

Undoes a per-child component override: if an `EntityModifier` exists for `childGuid` and holds an override for type `t`, removes it (via `EntityModifier.UndoCustomComponent`) so the child's own/prefab value shows through again. Returns `false` if there was no such modifier or override.

**Parameters** \
`childGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetChild(Guid, out EntityInstance&)

```csharp
public override bool TryGetChild(Guid guid, EntityInstance& instance)
```

Attempts to find the child with the given GUID, checking the base prefab's children first (unless `_ignorePrefabChildren` is set) before falling back to this instance's own added children. Returns `true` and populates `instance` if found in either place.

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
public override IComponent GetComponent(Type componentType)
```

Returns this instance's own override for `componentType` if one exists; otherwise falls back to `PrefabRef.Fetch().GetComponent(componentType)`. Throws if neither has a component of that type.

**Parameters** \
`componentType` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \

#### TryGetComponentForChild(Guid, Type)

```csharp
public override IComponent? TryGetComponentForChild(Guid guid, Type t)
```

Returns the component of type `t` from the child with GUID `guid`, checking any `EntityModifier` override for that child first, then the child's own value; returns `null` if neither has a component of that type or the child does not exist.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[IComponent](../../Bang/Components/IComponent.html) \

#### FetchChildren()

```csharp
public override ImmutableArray<T> FetchChildren()
```

Returns all the children of the base prefab, followed by all the children added by this instance (unless `_ignorePrefabChildren` is set, in which case only this instance's own children are returned).

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetChildComponents(Guid)

```csharp
public override ImmutableArray<T> GetChildComponents(Guid guid)
```

Fetch the effective components for the child identified by `guid` — resolved from either the prefab's own child or this instance's own child — with any `EntityModifier` for that child applied on top (additions/removals filtered in via `EntityModifier.FilterComponents`).

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Create(World, IEntity)

```csharp
public virtual int Create(World world, IEntity parent)
```

Inherited unchanged from `EntityInstance` — not overridden here. Creates this instance in `world`, using `parent`'s children modifiers (when `parent` is itself a `PrefabEntityInstance`) as an additional layer of overrides on top of this instance's own.

**Parameters** \
`world` [World](../../Bang/World.html) \
`parent` [IEntity](../../Murder/Prefabs/IEntity.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Create(World, Entity)

```csharp
public override int Create(World world, Entity? replaceEntity)
```

Resolves the full modifier chain for this instance — its own `_childrenModifiers`, merged with any modifiers coming from the prefab's own `PrefabEntityInstance` children, merged with any modifiers passed in from a parent — and hands the result and `PrefabRef.Guid` to `CreateInternal`/`EntityBuilder` to actually spawn (or, when `replaceEntity` is given, replace) the entity and its children in `world`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`replaceEntity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AddChild(EntityInstance)

```csharp
public virtual void AddChild(EntityInstance asset)
```

Inherited unchanged from `EntityInstance` — adds `asset` as a direct child of this prefab entity instance (as opposed to a child nested inside the prefab, which is instead handled through `AddChildAtChild`/`EntityModifier`).

**Parameters** \
`asset` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AddChildAtChild(Guid, EntityInstance)

```csharp
public virtual void AddChildAtChild(Guid childId, EntityInstance instance)
```

Adds `instance` as an extra child nested under the prefab child identified by `childId`, by creating (or reusing) an `EntityModifier` for that child and registering `instance` on it via `EntityModifier.AddChild`.

**Parameters** \
`childId` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`instance` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AddOrReplaceComponent(IComponent)

```csharp
public void AddOrReplaceComponent(IComponent c)
```

Adds or replaces component `c` as a per-instance override, affecting this instance's own entity (not one of its children). Not `virtual`/overridden — inherited directly from `EntityInstance`.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \

#### RemoveChildAtChild(Guid, Guid)

```csharp
public virtual void RemoveChildAtChild(Guid childId, Guid instance)
```

Removes the extra child identified by `instance` from the `EntityModifier` associated with the prefab child identified by `childId` (creating the modifier first if it did not already exist, which is a no-op in that case since there is nothing to remove).

**Parameters** \
`childId` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RemoveComponentForChild(Guid, Type)

```csharp
public override void RemoveComponentForChild(Guid instance, Type t)
```

Removes the component of type `t` from the child identified by `instance`: if it is one of this instance's own direct children, removes it there directly; otherwise records the removal in that child's `EntityModifier` (creating one if needed), so the component is filtered out wherever it is resolved from (the prefab or a further-nested child).

**Parameters** \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### SetName(string)

```csharp
public void SetName(string name)
```

Sets the display name of this entity instance. Not `virtual`/overridden — inherited directly from `EntityInstance`.

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

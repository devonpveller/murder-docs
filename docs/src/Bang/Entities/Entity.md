# Entity

**Namespace:** Bang.Entities \
**Assembly:** Bang.dll

```csharp
public class Entity : IDisposable
```

An entity is a collection of components within the world. This supports hierarchy (parent, children).

At its core, an `Entity` is little more than a stable [EntityId](#entityid) plus a bag of [IComponent](../../Bang/Components/IComponent.html) instances, keyed by the integer index that the world's `ComponentsLookup` assigns to each component type (see [BangComponentTypes](../../Bang/Entities/BangComponentTypes.html) for the handful of reserved indices). Entities have no public constructor: they only exist bound to a [World](../../Bang/World.html), which creates them and hands out the initial component array.

**Lifecycle**
- **Creation.** The world calls the internal constructor and then `InitializeComponents`, which registers every starting component, subscribes to any that implement `IModifiableComponent`, initializes any that implement [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html), and — in `World.DIAGNOSTICS_MODE` builds — asserts that components decorated with `RequiresAttribute` have their dependencies present.
- **Mutating components.** [AddComponent](#addcomponentt), [ReplaceComponent](#replacecomponenttintbool), [RemoveComponent](#removecomponentint) and [AddOrReplaceComponent](#addorreplacecomponenttint) are the building blocks; each has both a generic (`<T>`, compile-time type) and an untyped (`Type`/`IComponent`) overload for reflection-driven callers such as the editor. Index-based overloads (e.g. `AddComponent(T, int)`, `HasComponent(int)`) skip the type-to-index lookup and are the fastest path when the index is already known, such as from generated component extension code. Every successful mutation raises [OnComponentAdded](#oncomponentadded), [OnComponentModified](#oncomponentmodified) or [OnComponentRemoved](#oncomponentremoved) so systems and contexts can re-evaluate which entities they should track. `ReplaceComponent` skips the notification (and the write) entirely if the new value equals the old one, unless the component implements `IDoNotCheckOnReplaceTag` or `forceReplace` is passed.
- **The position fast path.** Because a `PositionComponent` is read on almost every entity every frame, it is cached directly on a private field instead of living only in the generic component dictionary, so [GetPosition](#getposition) can return it without a dictionary lookup or a boxing allocation. `HasComponent`, `AddComponent`, `RemoveComponent` and friends all special-case the `BangComponentTypes.Position` index to keep this cache in sync.
- **Parent/child hierarchy.** An entity may have at most one parent (see [Reparent](#reparententity) / [Unparent](#unparent)) and any number of children (see [AddChild](#addchildintstring) / [RemoveChild](#removechildstring)). Components that implement `IParentRelativeComponent` (such as `PositionComponent`) are automatically tracked against the parent: whenever the parent's copy of that component changes, `OnParentModified` recomputes the child's value (e.g. so a child's global position follows its parent). Destroying, activating or deactivating a parent recursively affects its children through the same event wiring.
- **Activation / deactivation.** [Activate](#activate) and [Deactivate](#deactivate) toggle [IsDeactivated](#isdeactivated) and notify the world so context filters stop (or resume) matching this entity, without removing any components. A child only follows its parent's (de)activation if it previously opted in via [SetActivateWithParent](#setactivatewithparent) (checked with [IsActivateWithParent](#isactivatewithparent)); by default parent and child activation states are independent.
- **Destruction.** [Destroy](#destroy) is a soft, immediate signal: it flips [IsDestroyed](#isdestroyed), notifies every component's removal (`OnComponentRemoved` with `causedByDestroy: true`) and fires [OnEntityDestroyed](#onentitydestroyed), but the entity is only fully wiped and recycled by the world at the end of the frame, via [Dispose](#dispose). Code that keeps a stale reference to a destroyed entity may therefore observe a "zombie" — an entity that reports `IsDestroyed == true` but whose fields have not all been cleared yet.
- **Messaging.** [SendMessage](#sendmessage) is a transient, one-frame broadcast: it marks the message's index as present (queryable via [HasMessage](#hasmessage)), fires [OnMessage](#onmessage) synchronously for any subscriber, and tells the world an entity has pending messages. Messages are not components — they are cleared every frame and should not be treated as persistent state; checking `HasMessage` from arbitrary code is discouraged because its result depends on system execution order within the frame.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Properties
#### Children
```csharp
public ImmutableArray<int> Children { get; }
```

Unique ids of all the children of the entity. This is computed lazily from the internal children map and cached until the set of children changes (a child is added or removed).

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Components
```csharp
public ImmutableArray<IComponent> Components { get; }
```

All the components currently active on this entity, as a fresh snapshot array. This is used by the editor and by serialization code; it is not meant for hot-path gameplay code, since it allocates and copies on every access.
            TODO: Optimize this. For now, this is okay since it's only used once the entity is serialized.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### EntityId
```csharp
public int EntityId { get; }
```

Entity unique identifier. Assigned once by the world when the entity is created and never changes, even if the entity is later reused/recycled by the world's id pool after being disposed.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### FetchChildrenWithNames
```csharp
public ImmutableDictionary<int, string?> FetchChildrenWithNames { get; }
```

Fetch a list of all the unique identifiers of the children with their respective names. Children added without an explicit name (see [AddChild](../../Bang/Entities/Entity.html)) map to a `null` name.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### IsActive
```csharp
public bool IsActive { get; }
```

Whether this entity is active or not. This is simply `!IsDeactivated && !IsDestroyed`; it does not have its own backing field.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsDeactivated
```csharp
public bool IsDeactivated { get; private set; }
```

Whether this entity has been deactivated or not. Toggled by [Activate](../../Bang/Entities/Entity.html) and [Deactivate](../../Bang/Entities/Entity.html); a deactivated entity keeps all of its components but is filtered out of context listeners until reactivated.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsDestroyed
```csharp
public bool IsDestroyed { get; private set; }
```

Whether this entity has been destroyed (and probably recycled) or not. Set by [Destroy](../../Bang/Entities/Entity.html) and never unset; a destroyed entity is awaiting final clean-up (see [Dispose](../../Bang/Entities/Entity.html)) at the end of the frame.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Parent
```csharp
public int? Parent { get; }
```

This is the unique id of the parent of the entity.
            Null if none (no parent).

**Returns** \
[int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
### ⭐ Events
#### OnComponentAdded
```csharp
public event Action<T1, T2> OnComponentAdded;
```

Fired whenever a new component is added. Sends the entity and the index of the component that was just added.

**Returns** \
[Action\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-2?view=net-7.0) \
#### OnComponentModified
```csharp
public event Action<T1, T2> OnComponentModified;
```

Fired whenever any component is replaced. Sends the entity and the index of the component that was just modified. This also fires for `IModifiableComponent` instances that raise a change internally, without going through `ReplaceComponent`.

**Returns** \
[Action\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-2?view=net-7.0) \
#### OnComponentRemoved
```csharp
public event Action<T1, T2, T3> OnComponentRemoved;
```

Fired whenever a new component is removed.
            This will send the entity, the component id that was just removed and
            whether this was caused by a destroy.

**Returns** \
[Action\<T1, T2, T3\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-3?view=net-7.0) \
#### OnEntityActivated
```csharp
public event Action<T> OnEntityActivated;
```

Fired when the entity gets activated, so it gets filtered
            back in the context listeners.

**Returns** \
[Action\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \
#### OnEntityDeactivated
```csharp
public event Action<T> OnEntityDeactivated;
```

Fired when the entity gets deactivated, so it is filtered out
            from its context listeners.

**Returns** \
[Action\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \
#### OnEntityDestroyed
```csharp
public event Action<T> OnEntityDestroyed;
```

Fired when the entity gets destroyed. Sends the entity id (not the entity instance, since by the time listeners further down the chain react, the entity may already be a zombie).

**Returns** \
[Action\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \
#### OnMessage
```csharp
public event Action<T1, T2, T3> OnMessage;
```

This will be fired when a message gets sent to the entity. Sends the entity, the message index and the message instance itself; the message is not retained after this call returns.

**Returns** \
[Action\<T1, T2, T3\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-3?view=net-7.0) \
### ⭐ Methods
#### AddComponent(T, int)
```csharp
public bool AddComponent(T c, int index)
```

Add a component `c` to the entity at a known `index`, skipping the component type lookup that `AddComponent(T)` performs. This is a no-op (and asserts, in debug builds) if the entity already has a component at `index` -- use [ReplaceComponent(T, int, bool)](../../Bang/Entities/Entity.html) for that instead.

**Parameters** \
`c` [T](../../) \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the component was added. Returns false if the entity was already destroyed or already had a component at `index`.

#### AddComponentOnce()
```csharp
public bool AddComponentOnce()
```

Add an empty component only once to the entity.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether a new component was added.
\

#### HasChild(int)
```csharp
public bool HasChild(int entityId)
```

Try to fetch a child with a <paramref name="entityId" /> entity identifier.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasChild(string)
```csharp
public bool HasChild(string name)
```

Try to fetch a child with a <paramref name="name" /> identifier

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

#### HasComponent()
```csharp
public bool HasComponent()
```

Whether this entity has a component of type T.
            This resolves T to its unique component index via the world's component lookup and then
            delegates to `HasComponent(int)`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponent(int)
```csharp
public bool HasComponent(int index)
```

Checks whether an entity has a component at a known `index`.
            This is the fastest of the `HasComponent` overloads: it is a direct bounds-checked
            lookup into the entity's internal availability table, with no type lookup involved.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponent(Type)
```csharp
public bool HasComponent(Type t)
```

Whether this entity has a component of type <paramref name="t" />.
            Prefer the generic `HasComponent<T>()` overload when the component type is known at
            compile time; this overload exists for reflection-driven callers (e.g. the editor) that
            only have a runtime `Type`.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasMessage()
```csharp
public bool HasMessage()
```

Whether entity has a message of type <typeparamref name="T" />.
            This should be avoided since it highly depends on the order of the systems
            being fired and can lead to several bugs.
            For example, if we check for that on the state machine, it will depend on the order
            of the entities in the world.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasMessage(int)
```csharp
public bool HasMessage(int index)
```

Whether entity has a message of index <paramref name="index" />.
            This should be avoided since it highly depends on the order of the systems
            being fired and can lead to several bugs.
            For example, if we check for that on the state machine, it will depend on the order
            of the entities in the world.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsActivateWithParent()
```csharp
public bool IsActivateWithParent()
```

Whether this entity should be reactivated with the parent.
            This is used when serializing data and we might need to revisit this soon.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveChild(string)
```csharp
public bool RemoveChild(string name)
```

Remove a child, identified by `name`, from the entity.
            This unparents the child (see [Unparent](../../Bang/Entities/Entity.html)) but does not destroy it.
            This is a no-op if no child with that name is currently tracked.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether a child with that name was found and removed.

#### RemoveComponent()
```csharp
public bool RemoveComponent()
```

Removes component of type <typeparamref name="T" />.
            Do nothing if <typeparamref name="T" /> is not owned by this entity.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveComponent(int)
```csharp
public bool RemoveComponent(int index)
```

Remove a component from the entity.
            Returns true if the element existed and was removed.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveMessage(int)
```csharp
public bool RemoveMessage(int index)
```

This removes a message from the entity. This is used when the message must be removed within
            this frame.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RenameChild(string, string)
```csharp
public bool RenameChild(string previousName, string newName)
```

Rename an existing child.

**Parameters** \
`previousName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`newName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether it succeeded (e.g. `previousName` exists).

#### ReplaceComponent(T, int, bool)
```csharp
public bool ReplaceComponent(T c, int index, bool forceReplace)
```

Replace a component from the entity.
            Returns true if the element existed and was replaced. If the entity is destroyed, or if
            there is no component at `index` yet, this is a no-op that returns false. Unless
            `forceReplace` is passed (or the component implements `IDoNotCheckOnReplaceTag`), replacing
            a component with a value that equals the previous one is also skipped -- no write, no
            notification.

**Parameters** \
`c` [T](../../) \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`forceReplace` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetComponent(out T&)
```csharp
public bool TryGetComponent(T& component)
```

Try to get a component of type T without asserting.
            Unlike [GetComponent()](../../Bang/Entities/Entity.html), this is safe to call when the entity may or may not
            have the component.

**Parameters** \
`component` [T&](../../) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the entity had a component of type T.

#### TryGetComponent(Type, out T&)
```csharp
public bool TryGetComponent(Type t, IComponent& component)
```

Method used by editor to retrieve specific components defined in runtime.
            DO NOT use this in game -- prefer the generic `TryGetComponent<T>(out T?)` overload, which
            avoids the `Type` lookup and the cast.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`component` [IComponent&](../../Bang/Components/IComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AddComponent(T)
```csharp
public Entity AddComponent(T c)
```

Add component `c` to this entity. If the world has not been initialized yet (the entity is still
            being built up before being handed to the world), the component is appended with an
            arbitrary index instead of its real component index, and will be re-indexed once the
            entity is initialized.

**Parameters** \
`c` [T](../../) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
Entity (this), to allow chaining multiple `AddComponent` calls.

#### TryFetchChild(int)
```csharp
public Entity TryFetchChild(int id)
```

Try to fetch a child with a <paramref name="id" /> identifier

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryFetchChild(string)
```csharp
public Entity TryFetchChild(string name)
```

Try to fetch a child with a <paramref name="name" /> identifier

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
\

#### TryFetchChildWithComponent()
```csharp
public Entity TryFetchChildWithComponent()
```

This fetches a child with a given component.
            TODO: Optimize, or cache?

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryFetchParent()
```csharp
public Entity TryFetchParent()
```

Try to fetch the parent entity.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
\

#### GetComponent()
```csharp
public T GetComponent()
```

Fetch a component of type T. If the entity does not have that component, this method will assert and fail.

**Returns** \
[T](../../) \

#### GetComponent(int)
```csharp
public T GetComponent(int index)
```

Fetch a component of type T with <paramref name="index" />. 
            If the entity does not have that component, this method will assert and fail.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T](../../) \

#### TryGetComponent()
```csharp
public T? TryGetComponent()
```

Try to get a component of type T. If the entity does not have it, returns null instead of asserting.
            Restricted to struct component types so the "no component" case can be represented as a
            genuine null instead of a zeroed-out struct that could be confused with a real value.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### GetPosition()
```csharp
public PositionComponent GetPosition()
```

Fetch the position component directly.
            If the entity does not have that component, this method will assert and fail.
            Since we fetch position so often, this will bypass a boxing operation by asking for the
            position directly from a cached field rather than through the generic component dictionary.

**Returns** \
[PositionComponent](../../Murder/Components/PositionComponent.html) \

#### Dispose()
```csharp
public virtual void Dispose()
```

Dispose the entity.
            This will unparent and remove all components.
            It also removes subscription from all their contexts or entities.

#### Activate()
```csharp
public void Activate()
```

Marks an entity as active if it isn't already.

#### AddChild(int, string)
```csharp
public void AddChild(int id, string name)
```

Assign an existing entity as a child.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

#### AddComponent(IComponent, Type)
```csharp
public void AddComponent(IComponent c, Type t)
```

Add a component <paramref name="c" /> of type <paramref name="t" />.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \
\
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
\

#### AddOrReplaceComponent(IComponent, Type)
```csharp
public void AddOrReplaceComponent(IComponent c, Type t)
```

Add or replace component of type <paramref name="t" /> with <paramref name="c" />.
            Do nothing if the entity has been destroyed.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \
\
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
\

#### AddOrReplaceComponent(T, int)
```csharp
public void AddOrReplaceComponent(T c, int index)
```

Add or replace component of type T with <paramref name="c" /> at a known <paramref name="index" />.
            Do nothing if the entity has been destroyed.

**Parameters** \
`c` [T](../../) \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AddOrReplaceComponent(T)
```csharp
public void AddOrReplaceComponent(T c)
```

Add or replace component of type T with <paramref name="c" />.
            Do nothing if the entity has been destroyed.

**Parameters** \
`c` [T](../../) \

#### Deactivate()
```csharp
public void Deactivate()
```

Marks an entity as deactivated if it isn't already.

#### Destroy()
```csharp
public void Destroy()
```

Destroy the entity from the world.
            This will notify all components that it will be removed from the entity.
            At the end of the update of the frame, it will wipe this entity from the world.
            However, if someone still holds reference to an [Entity](../../Bang/Entities/Entity.html) (they shouldn't),
            they might see a zombie entity after this.

#### RemoveChild(int)
```csharp
public void RemoveChild(int id)
```

Remove a child, identified by <paramref name="id" />, from the entity.
            This unparents the child (see [Unparent](../../Bang/Entities/Entity.html)) but does not destroy it.
            This is a no-op if <paramref name="id" /> is not currently tracked as a child, or if this
            entity has already been destroyed (to avoid mutating collections mid-teardown).

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RemoveComponent(Type)
```csharp
public void RemoveComponent(Type t)
```

Removes component of type <paramref name="t" />.
            Do nothing if <paramref name="t" /> is not owned by this entity.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
\

#### Reparent(Entity)
```csharp
public void Reparent(Entity parent)
```

Set the parent of this entity.

**Parameters** \
`parent` [Entity](../../Bang/Entities/Entity.html) \

#### Replace(IComponent[], List<T>, bool)
```csharp
public void Replace(IComponent[] components, List<T> children, bool wipe)
```

Replace all the components of the entity. This is useful when you want to reuse
            the same entity id with new components.

**Parameters** \
`components` [IComponent[]](../../Bang/Components/IComponent.html) \
\
`children` [List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \
\
`wipe` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

#### ReplaceComponent(IComponent, Type, bool)
```csharp
public void ReplaceComponent(IComponent c, Type t, bool forceReplace)
```

Replace componenent of type <paramref name="t" /> with <paramref name="c" />.
            This asserts if the component does not exist or is not assignable from <paramref name="t" />.
            Do nothing if the entity has been destroyed.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \
\
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
\
`forceReplace` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

#### ReplaceComponent(T)
```csharp
public void ReplaceComponent(T c)
```

Replace componenent of type T with <paramref name="c" />.
            This asserts if the component does not exist or is not assignable from T.
            Do nothing if the entity has been destroyed.

**Parameters** \
`c` [T](../../) \

#### SendMessage()
```csharp
public void SendMessage()
```

Sends a message of type <typeparamref name="T" /> for any system watching it.

#### SendMessage(int, T)
```csharp
public void SendMessage(int index, T message)
```

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`message` [T](../../) \

#### SendMessage(T)
```csharp
public void SendMessage(T message)
```

**Parameters** \
`message` [T](../../) \

#### SetActivateWithParent()
```csharp
public void SetActivateWithParent()
```

Force the entity to be activated and propagated according to the parent. Default is false (they are independent!)

#### Unparent()
```csharp
public void Unparent()
```

This will remove a parent of the entity.
            It untracks all the tracked components and removes itself from the parent's children.



⚡
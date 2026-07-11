# World

**Namespace:** Bang \
**Assembly:** Bang.dll

```csharp
public class World : IDisposable
```

This is the internal representation of a world within ECS.
            A world has the knowledge of all the entities and all the systems that exist within the game.
            This handles dispatching information and handling disposal of entities.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors
```csharp
public World(IList<T> systems)
```

Initialize the world!

**Parameters** \
`systems` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \
List of systems and whether they are currently active in the world. \

**Exceptions** \
[ArgumentException](https://learn.microsoft.com/en-us/dotnet/api/System.ArgumentException?view=net-7.0) \
If no systems are passed to the world. \
### ⭐ Properties
#### _cachedRenderSystems
```csharp
protected readonly SortedList<TKey, TValue> _cachedRenderSystems;
```

This must be called by engine implementations of Bang to handle with rendering.

**Returns** \
[SortedList\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.SortedList-2?view=net-7.0) \
#### _overallStopwatch
```csharp
protected readonly Stopwatch _overallStopwatch;
```

This is the stopwatch used on all systems when monitoring performance. Only used if [World.DIAGNOSTICS_MODE](../Bang/World.html#diagnostics_mode) is set.

**Returns** \
[Stopwatch](https://learn.microsoft.com/en-us/dotnet/api/System.Diagnostics.Stopwatch?view=net-7.0) \
#### _stopwatch
```csharp
protected readonly Stopwatch _stopwatch;
```

This is the stopwatch used per systems when monitoring performance. Only used if [World.DIAGNOSTICS_MODE](../Bang/World.html#diagnostics_mode) is set.

**Returns** \
[Stopwatch](https://learn.microsoft.com/en-us/dotnet/api/System.Diagnostics.Stopwatch?view=net-7.0) \
#### Contexts
```csharp
protected readonly Dictionary<TKey, TValue> Contexts;
```

Maps all the context IDs with the context.
            We might add new ones if a system calls for a new context filter.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### DIAGNOSTICS_MODE
```csharp
public static bool DIAGNOSTICS_MODE;
```

Use this to set whether diagnostics should be pulled from the world run.

While enabled, each [World](../Bang/World.html) measures how long every startup, update, fixed update
and reactive system takes to run (see [World.StartCounters](../Bang/World.html#startcounters), [World.UpdateCounters](../Bang/World.html#updatecounters),
[World.FixedUpdateCounters](../Bang/World.html#fixedupdatecounters) and [World.ReactiveCounters](../Bang/World.html#reactivecounters)) and runs extra
assertion sanity checks (e.g. validating system requirements declared via [RequiresAttribute](../Bang/Components/RequiresAttribute.html)).
This is a static, process-wide flag: disable it for release builds where the extra bookkeeping is not
worth the overhead.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### EntityCount
```csharp
public int EntityCount { get; }
```

Total of entities in the world. This is useful for displaying debug information.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### FixedUpdateCounters
```csharp
public readonly Dictionary<TKey, TValue> FixedUpdateCounters;
```

This has the duration of each fixed update system (id) to its corresponding time (in ms).
            See [World.IdToSystem](../Bang/World.html#idtosystem) on how to fetch the actual system.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### IdToSystem
```csharp
public readonly ImmutableDictionary<TKey, TValue> IdToSystem;
```

Used when fetching systems based on its unique identifier.
            Maps: System order id -&gt; System instance.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### IsExiting
```csharp
public bool IsExiting { get; private set; }
```

Whether the world is currently being exited, e.g. [World.Exit](../Bang/World.html#exit) was called.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsPaused
```csharp
public bool IsPaused { get; private set; }
```

Whether the world has been queried to be on pause or not.
            See [World.Pause](../Bang/World.html#pause).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### NextEligibleEntityId
```csharp
public int NextEligibleEntityId { get; set; }
```

Expose the next eligible entity id.

Reading this returns the id that will be assigned to the next entity created without an explicit id.
Setting it will only ever raise the counter (it takes the maximum of the current value and the assigned
value), which is used when restoring a world from a save so that newly created entities never collide
with previously serialized ids.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### ReactiveCounters
```csharp
public readonly Dictionary<TKey, TValue> ReactiveCounters;
```

This has the duration of each reactive system (id) to its corresponding time (in ms).
            See [World.IdToSystem](../Bang/World.html#idtosystem) on how to fetch the actual system.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### StartCounters
```csharp
public readonly Dictionary<TKey, TValue> StartCounters;
```

This has the duration of each start system (id) to its corresponding time (in ms).
            See [World.IdToSystem](../Bang/World.html#idtosystem) on how to fetch the actual system.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### UpdateCounters
```csharp
public readonly Dictionary<TKey, TValue> UpdateCounters;
```

This has the duration of each update system (id) to its corresponding time (in ms).
            See [World.IdToSystem](../Bang/World.html#idtosystem) on how to fetch the actual system.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
### ⭐ Methods
#### ClearDiagnosticsCountersForSystem(int)
```csharp
protected virtual void ClearDiagnosticsCountersForSystem(int systemId)
```

Implemented by custom world in order to clear diagnostic information about the world.
Called whenever `systemId` is deactivated, right after its built-in performance counters
([World.StartCounters](../Bang/World.html#startcounters), [World.UpdateCounters](../Bang/World.html#updatecounters), [World.FixedUpdateCounters](../Bang/World.html#fixedupdatecounters) and [World.ReactiveCounters](../Bang/World.html#reactivecounters)) have
been cleared. No-op by default.

**Parameters** \
`systemId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Order id of the system being deactivated, as tracked by [World.IdToSystem](../Bang/World.html#idtosystem). \

#### InitializeDiagnosticsForSystem(int, ISystem)
```csharp
protected virtual void InitializeDiagnosticsForSystem(int systemId, ISystem system)
```

Implemented by custom world in order to express diagnostic information about the world.
Called once per system while [World.InitializeDiagnosticsCounters](../Bang/World.html#initializediagnosticscounters) sets up the built-in performance
counters, so a custom world can register its own extra diagnostics for `system` alongside them.
No-op by default.

**Parameters** \
`systemId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Order id of `system`, as tracked by [World.IdToSystem](../Bang/World.html#idtosystem). \
`system` [ISystem](../Bang/Systems/ISystem.html) \
The system instance being initialized. \

#### InitializeDiagnosticsCounters()
```csharp
protected void InitializeDiagnosticsCounters()
```

Initialize the performance counters according to the systems present in the world.

#### ActivateSystem()
```csharp
public bool ActivateSystem()
```

Activate a system of type `T` within our world. `T` must have been passed to the world's constructor.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the system is found and has been activated.

#### ActivateSystem(Type)
```csharp
public bool ActivateSystem(Type t, bool immediately)
```

Activate a system of type <paramref name="t" /> within our world.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
Type of the system to activate. \
`immediately` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the activation should take effect right away. When `false` (the default), the system is only
queued and will actually be activated at the end of the current [World.Update](../Bang/World.html#update) or [World.Start](../Bang/World.html#start) call. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the system is found and has been activated.

#### DeactivateSystem(bool)
```csharp
public bool DeactivateSystem(bool immediately)
```

Deactivate a system of type `T` within our world. `T` must have been passed to the world's constructor.

**Parameters** \
`immediately` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the deactivation should take effect right away. When `false` (the default), the system is only
queued and will actually be deactivated at the end of the current [World.Update](../Bang/World.html#update) or [World.Start](../Bang/World.html#start) call. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the system is found and has been deactivated.

#### DeactivateSystem(int, bool)
```csharp
public bool DeactivateSystem(int id, bool immediately)
```

Deactivate a system with the given order <paramref name="id" /> within our world.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Order id of the system, as tracked by [World.IdToSystem](../Bang/World.html#idtosystem). \
`immediately` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the deactivation should take effect right away. When `false` (the default), the system is only
queued and will actually be deactivated at the end of the current [World.Update](../Bang/World.html#update) or [World.Start](../Bang/World.html#start) call. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the system was active and has now been deactivated (or queued for deactivation).

#### DeactivateSystem(Type, bool)
```csharp
public bool DeactivateSystem(Type t, bool immediately)
```

Deactivate a system of type <paramref name="t" /> within our world.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
Type of the system to deactivate. \
`immediately` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the deactivation should take effect right away. When `false` (the default), the system is only
queued and will actually be deactivated at the end of the current [World.Update](../Bang/World.html#update) or [World.Start](../Bang/World.html#start) call. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether the system is found and has been deactivated.

#### IsSystemActive(Type)
```csharp
public bool IsSystemActive(Type t)
```

Whether a system is active within the world.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### InitializeLookupComponents(ComponentsLookup)
```csharp
public static void InitializeLookupComponents(ComponentsLookup lookup)
```

Explicitly set the [ComponentsLookup](../Bang/ComponentsLookup.html) implementation that all worlds in this process will use, bypassing
the reflection-based lookup performed by [World.FindLookupImplementation](../Bang/World.html#findlookupimplementation).
This is useful for tests or tools that create a [World](../Bang/World.html) before all the generated assemblies have been
loaded into the `AppDomain`. Once set, this value is cached for the remainder of the process.

**Parameters** \
`lookup` [ComponentsLookup](../Bang/ComponentsLookup.html) \
The generated [ComponentsLookup](../Bang/ComponentsLookup.html) instance to use. \

#### FindLookupImplementation()
```csharp
public static ComponentsLookup FindLookupImplementation()
```

Look for an implementation for the lookup table of components.

The result is cached the first time this is called (or if [World.InitializeLookupComponents](../Bang/World.html#initializelookupcomponentscomponentslookup) was called
beforehand). Otherwise, this scans every currently loaded assembly in the `AppDomain` for concrete types
that derive from [ComponentsLookup](../Bang/ComponentsLookup.html) and picks the one with the deepest inheritance chain (i.e. the most
specific generated lookup, such as a game-specific lookup that inherits from Bang's own generated lookup).

**Returns** \
[ComponentsLookup](../Bang/ComponentsLookup.html) \

**Exceptions** \
[InvalidOperationException](https://learn.microsoft.com/en-us/dotnet/api/System.InvalidOperationException?view=net-7.0) \
Thrown if no [ComponentsLookup](../Bang/ComponentsLookup.html) implementation could be found, which usually means the source generator
has not run for the project. \

#### AddEntity()
```csharp
public Entity AddEntity()
```

Add a new empty entity to the world. 
            This will map the instance to the world.
            Any components added after this entity has been created will be notified to any reactive systems.

**Returns** \
[Entity](../Bang/Entities/Entity.html) \

#### AddEntity(IComponent[])
```csharp
public Entity AddEntity(IComponent[] components)
```

Add a single entity to the world (e.g. collection of <paramref name="components" />). 
            This will map the instance to the world.

**Parameters** \
`components` [IComponent[]](../Bang/Components/IComponent.html) \

**Returns** \
[Entity](../Bang/Entities/Entity.html) \

#### AddEntity(T?, IComponent[])
```csharp
public Entity AddEntity(T? id, IComponent[] components)
```

**Parameters** \
`id` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`components` [IComponent[]](../Bang/Components/IComponent.html) \

**Returns** \
[Entity](../Bang/Entities/Entity.html) \

#### GetEntity(int)
```csharp
public Entity GetEntity(int id)
```

Get an entity with the specific id.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Entity](../Bang/Entities/Entity.html) \

#### GetUniqueEntity()
```csharp
public Entity GetUniqueEntity()
```

Call [World.GetUniqueEntity(int)](../Bang/World.html#getuniqueentityint) from a generator instead.

**Returns** \
[Entity](../Bang/Entities/Entity.html) \

#### GetUniqueEntity(int)
```csharp
public Entity GetUniqueEntity(int index)
```

Get an entity with the unique component <typeparamref name="T" />.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Entity](../Bang/Entities/Entity.html) \

#### TryGetEntity(int)
```csharp
public Entity TryGetEntity(int id)
```

Tries to get an entity with the specific id.
            If the entity is no longer among us, return null.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Entity](../Bang/Entities/Entity.html) \

#### TryGetUniqueEntity()
```csharp
public Entity TryGetUniqueEntity()
```

Call [World.TryGetUniqueEntity(int)](../Bang/World.html#trygetuniqueentityint) from a generator instead.

**Returns** \
[Entity](../Bang/Entities/Entity.html) \

#### TryGetUniqueEntity(int)
```csharp
public Entity TryGetUniqueEntity(int index)
```

Try to get a unique entity that owns <typeparamref name="T" />.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Entity](../Bang/Entities/Entity.html) \

#### GetActivatedAndDeactivatedEntitiesWith(Type[])
```csharp
public ImmutableArray<T> GetActivatedAndDeactivatedEntitiesWith(Type[] components)
```

This is very slow. It should get both the activate an deactivate entities.
            Used when it is absolutely necessary to get both activate and deactivated entities on the filtering.

**Parameters** \
`components` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetAllEntities()
```csharp
public ImmutableArray<T> GetAllEntities()
```

This should be used very cautiously! I hope you know what you are doing.
            It fetches all the entities within the world and return them.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetAllDeactivatedEntities()
```csharp
public ImmutableArray<T> GetAllDeactivatedEntities()
```

This should be used very cautiously! I hope you know what you are doing.
            It fetches all the deactivated entities within the world and return them.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetEntitiesFrom(int)
```csharp
public ImmutableArray<T> GetEntitiesFrom(int contextId)
```

Retrieve the entities tracked by an already existing context, given its <paramref name="contextId" />.
Unlike [World.GetEntitiesWith(ContextAccessorFilter, Type[])](../Bang/World.html#getentitieswithcontextaccessorfilter-type), this does not create a new context on demand — the context
must have already been created (e.g. via a prior call to [World.GetEntitiesWith(ContextAccessorFilter, Type[])](../Bang/World.html#getentitieswithcontextaccessorfilter-type)
or [World.GetOrCreateContextIdFrom](../Bang/World.html#getorcreatecontextidfromcontextaccessorfilter-type)). If `contextId` does not map to a known context, this will
assert and return an empty array.

**Parameters** \
`contextId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Id of a context previously created within this world. \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### TryGetEntitiesFrom(int, out ImmutableArray<T>&)
```csharp
public bool TryGetEntitiesFrom(int contextId, ImmutableArray<T>& entities)
```

Try to retrieve the entities tracked by an already existing context, given its <paramref name="contextId" />.

**Parameters** \
`contextId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Id of a context previously created within this world. \
`entities` [ImmutableArray\<T\>&](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
The entities tracked by the context, if found. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether a context with `contextId` exists.

#### GetOrCreateContextIdFrom(ContextAccessorFilter, Type[])
```csharp
public int GetOrCreateContextIdFrom(ContextAccessorFilter filter, Type[] components)
```

Retrieve a context ID for the specified filter and components.

**Parameters** \
`filter` [ContextAccessorFilter](../Bang/Contexts/ContextAccessorFilter.html) \
`components` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetEntitiesWith(ContextAccessorFilter, Type[])
```csharp
public ImmutableArray<T> GetEntitiesWith(ContextAccessorFilter filter, Type[] components)
```

Retrieve all the entities that match <paramref name="filter" /> for <paramref name="components" />.
The underlying context is created lazily on first use and cached for subsequent calls with the same
filter and component set.

**Parameters** \
`filter` [ContextAccessorFilter](../Bang/Contexts/ContextAccessorFilter.html) \
Whether entities must have all, any, or none of `components`. \
`components` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
Component types to filter entities by. \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetEntitiesWith(Type[])
```csharp
public ImmutableArray<T> GetEntitiesWith(Type[] components)
```

Retrieve all the entities that have all of <paramref name="components" />. Equivalent to calling
[World.GetEntitiesWith(ContextAccessorFilter, Type[])](../Bang/World.html#getentitieswithcontextaccessorfilter-type) with [ContextAccessorFilter.AllOf](../Bang/Contexts/ContextAccessorFilter.html#allof).

**Parameters** \
`components` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
Component types the entities must all have. \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetUnique()
```csharp
public T GetUnique()
```

Call [World.GetUnique(int)](../Bang/World.html#getuniqueint) from a generator instead.

**Returns** \
[T](../) \

#### GetUnique(int)
```csharp
public T GetUnique(int index)
```

Get the unique component <typeparamref name="T" /> within an entity. The component has index of <paramref name="index" />.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

**Returns** \
[T](../) \

#### TryGetUnique()
```csharp
public T? TryGetUnique()
```

Call [World.TryGetUnique(int)](../Bang/World.html#trygetuniqueint) from a generator instead.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### TryGetUnique(int)
```csharp
public T? TryGetUnique(int index)
```

Try to get a unique entity that owns <typeparamref name="T" />. The component has index of <paramref name="index" />.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
\

#### Dispose()
```csharp
public virtual void Dispose()
```

This will first call all [IExitSystem](../Bang/Systems/IExitSystem.html) to cleanup each system. 
            It will then call Dispose on each of the entities on the world and clear all the collections.

#### Pause()
```csharp
public virtual void Pause()
```

Pause all the set of systems that qualify in [World.IsPauseSystem(Bang.Systems.ISystem)](../Bang/World.html).
            A paused system will no longer be called on any [World.Update](../Bang/World.html#update) calls.

#### Resume()
```csharp
public virtual void Resume()
```

This will resume all paused systems.

#### ActivateAllSystems()
```csharp
public void ActivateAllSystems()
```

Activate all systems across the world.

#### DeactivateAllSystems(Type[])
```csharp
public void DeactivateAllSystems(Type[] skip)
```

Deactivate all systems across the world.

**Parameters** \
`skip` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
Any system whose type matches (or derives from) one of these types will be left untouched. \

#### Exit()
```csharp
public void Exit()
```

Call to end all systems.
            This is called right before shutting down or switching scenes.

#### FixedUpdate()
```csharp
public void FixedUpdate()
```

Calls update on all [IFixedUpdateSystem](../Bang/Systems/IFixedUpdateSystem.html) systems.
            This will be called on fixed intervals.

#### Start()
```csharp
public void Start()
```

Call start on all systems.
            This is called before any updates and will notify any reactive systems by the end of it.

#### Update()
```csharp
public void Update()
```

Calls update on all [IUpdateSystem](../Bang/Systems/IUpdateSystem.html) systems.
            At the end of update, it will notify all reactive systems of any changes made to entities
            they were watching.
            Finally, it destroys all pending entities and clear all messages.



⚡
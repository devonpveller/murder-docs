# MonoWorld

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class MonoWorld : World, IDisposable
```

World implementation based in MonoGame.

**Intent:** The Murder ECS world that owns all entities, systems, and the camera for a single loaded level.

**Use-case:** Created automatically by `GameScene.LoadContentImpl` from a `WorldAsset`. Use it to add/query entities, toggle systems, or access the camera from within any system.

**Implements:** _[World](../../Bang/World.html), [IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
public MonoWorld(IList<T> systems, Camera2D camera, Guid worldAssetGuid)
```

**Parameters** \
`systems` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \
`camera` [Camera2D](../../Murder/Core/Graphics/Camera2D.html) \
`worldAssetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### \_cachedRenderSystems

```csharp
protected readonly SortedList<TKey, TValue> _cachedRenderSystems;
```

Cached sorted list of render-capable systems, keyed by render order, used each frame to drive draw calls without re-querying the system list.

**Returns** \
[SortedList\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.SortedList-2?view=net-7.0) \

#### \_overallStopwatch

```csharp
protected readonly Stopwatch _overallStopwatch;
```

Measures total elapsed time for the world update cycle when diagnostics are enabled.

**Returns** \
[Stopwatch](https://learn.microsoft.com/en-us/dotnet/api/System.Diagnostics.Stopwatch?view=net-7.0) \

#### \_stopwatch

```csharp
protected readonly Stopwatch _stopwatch;
```

Measures per-system elapsed time when diagnostics are enabled.

**Returns** \
[Stopwatch](https://learn.microsoft.com/en-us/dotnet/api/System.Diagnostics.Stopwatch?view=net-7.0) \

#### Camera

```csharp
public readonly Camera2D Camera;
```

The 2D camera associated with this world, used by render systems to determine the visible viewport.

**Returns** \
[Camera2D](../../Murder/Core/Graphics/Camera2D.html) \

#### Contexts

```csharp
protected readonly Dictionary<TKey, TValue> Contexts;
```

Maps each system context ID to its `IComponentContext`, allowing systems to query the entities relevant to them.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### EntityCount

```csharp
public int EntityCount { get; }
```

The total number of entities currently alive in this world.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### FixedUpdateCounters

```csharp
public readonly Dictionary<TKey, TValue> FixedUpdateCounters;
```

Maps each fixed-update system ID to its timing data (duration in ms per tick). See `World.IdToSystem` to resolve IDs.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### GuiCounters

```csharp
public readonly Dictionary<TKey, TValue> GuiCounters;
```

This has the duration of each gui render system (id) to its corresponding time (in ms).
See [World.IdToSystem](../../Bang/World.html#idtosystem) on how to fetch the actual system.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### IdToSystem

```csharp
public readonly ImmutableDictionary<TKey, TValue> IdToSystem;
```

Immutable mapping from system integer ID to the `ISystem` instance, used to look up systems by ID in diagnostics counters.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### IsExiting

```csharp
public bool IsExiting { get; }
```

Whether the world has been requested to exit and is in the process of shutting down.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsPaused

```csharp
public bool IsPaused { get; }
```

Whether the world is currently paused; when `true`, update systems do not tick.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PreRenderCounters

```csharp
public readonly Dictionary<TKey, TValue> PreRenderCounters;
```

This has the duration of each reactive system (id) to its corresponding time (in ms).
See [World.IdToSystem](../../Bang/World.html#idtosystem) on how to fetch the actual system.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### ReactiveCounters

```csharp
public readonly Dictionary<TKey, TValue> ReactiveCounters;
```

Maps each reactive system ID to its timing data (duration in ms per message batch). See `World.IdToSystem` to resolve IDs.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### RenderCounters

```csharp
public readonly Dictionary<TKey, TValue> RenderCounters;
```

This has the duration of each render system (id) to its corresponding time (in ms).
See [World.IdToSystem](../../Bang/World.html#idtosystem) on how to fetch the actual system.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### StartCounters

```csharp
public readonly Dictionary<TKey, TValue> StartCounters;
```

Maps each start system ID to its timing data (duration in ms for its initial start call). See `World.IdToSystem` to resolve IDs.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### UpdateCounters

```csharp
public readonly Dictionary<TKey, TValue> UpdateCounters;
```

Maps each update system ID to its timing data (duration in ms per frame). See `World.IdToSystem` to resolve IDs.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### WorldAssetGuid

```csharp
public readonly Guid WorldAssetGuid;
```

The GUID of the `WorldAsset` from which this world was instantiated.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Methods

#### ClearDiagnosticsCountersForSystem(int)

```csharp
protected virtual void ClearDiagnosticsCountersForSystem(int id)
```

Clears the diagnostics timing counters for the system with the given ID.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### InitializeDiagnosticsForSystem(int, ISystem)

```csharp
protected virtual void InitializeDiagnosticsForSystem(int systemId, ISystem system)
```

Registers a system in the diagnostics counters dictionaries so it can be tracked.

**Parameters** \
`systemId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`system` [ISystem](../../Bang/Systems/ISystem.html) \

#### InitializeDiagnosticsCounters()

```csharp
protected void InitializeDiagnosticsCounters()
```

Initializes all per-system diagnostics counter dictionaries.

#### ActivateSystem()

```csharp
public bool ActivateSystem()
```

Activates the system of the generic type parameter in this world.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ActivateSystem(Type)

```csharp
public bool ActivateSystem(Type t)
```

Activates the system of the specified type in this world.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DeactivateSystem(bool)

```csharp
public bool DeactivateSystem(bool immediately)
```

Deactivates the system of the generic type parameter. If `immediately` is `true`, the system is disabled before the next update.

**Parameters** \
`immediately` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DeactivateSystem(int, bool)

```csharp
public bool DeactivateSystem(int id, bool immediately)
```

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`immediately` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DeactivateSystem(Type, bool)

```csharp
public bool DeactivateSystem(Type t, bool immediately)
```

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`immediately` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsSystemActive(Type)

```csharp
public bool IsSystemActive(Type t)
```

Returns `true` when the system of type `t` is currently active in this world.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AddEntity()

```csharp
public Entity AddEntity()
```

Creates a new empty entity in the world and returns it.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### AddEntity(IComponent[])

```csharp
public Entity AddEntity(IComponent[] components)
```

Creates a new entity initialized with the given components.

**Parameters** \
`components` [IComponent[]](../../Bang/Components/IComponent.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### AddEntity(T?, IComponent[])

```csharp
public Entity AddEntity(T? id, IComponent[] components)
```

Creates a new entity with an optional integer ID hint and the given components.

**Parameters** \
`id` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`components` [IComponent[]](../../Bang/Components/IComponent.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### GetEntity(int)

```csharp
public Entity GetEntity(int id)
```

Retrieves the entity with the given ID. Throws if not found.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### GetUniqueEntity()

```csharp
public Entity GetUniqueEntity()
```

Retrieves the single entity that uniquely holds a component of the generic type. Throws if not found.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### GetUniqueEntity(int)

```csharp
public Entity GetUniqueEntity(int index)
```

Retrieves the unique entity for the specified context index. Throws if not found.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryGetEntity(int)

```csharp
public Entity TryGetEntity(int id)
```

Retrieves the entity with the given ID, or `null` if it does not exist.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryGetUniqueEntity()

```csharp
public Entity TryGetUniqueEntity()
```

Returns the unique entity that holds a component of the generic type, or `null` if none exists.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryGetUniqueEntity(int)

```csharp
public Entity TryGetUniqueEntity(int index)
```

Returns the unique entity for the specified context index, or `null` if none exists.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### GetActivatedAndDeactivatedEntitiesWith(Type[])

```csharp
public ImmutableArray<T> GetActivatedAndDeactivatedEntitiesWith(Type[] components)
```

Returns all entities (both active and deactivated) that possess all of the specified component types.

**Parameters** \
`components` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetAllEntities()

```csharp
public ImmutableArray<T> GetAllEntities()
```

Returns all active entities in the world.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetEntitiesWith(ContextAccessorFilter, Type[])

```csharp
public ImmutableArray<T> GetEntitiesWith(ContextAccessorFilter filter, Type[] components)
```

Returns entities that match the given component filter.

**Parameters** \
`filter` [ContextAccessorFilter](../../Bang/Contexts/ContextAccessorFilter.html) \
`components` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetEntitiesWith(Type[])

```csharp
public ImmutableArray<T> GetEntitiesWith(Type[] components)
```

Returns all active entities that possess all of the given component types.

**Parameters** \
`components` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetUnique()

```csharp
public T GetUnique()
```

Returns the unique component of the generic type from its singleton entity. Throws if not found.

**Returns** \
[T](../../) \

#### GetUnique(int)

```csharp
public T GetUnique(int index)
```

Returns the unique component for the specified context index. Throws if not found.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T](../../) \

#### TryGetUnique()

```csharp
public T? TryGetUnique()
```

Returns the unique component of the generic type, or the default value if no matching singleton entity exists.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### TryGetUnique(int)

```csharp
public T? TryGetUnique(int index)
```

Returns the unique component for the specified context index, or the default value if not found.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Dispose()

```csharp
public virtual void Dispose()
```

Disposes the world and all of its entities and systems.

#### Pause()

```csharp
public virtual void Pause()
```

Pauses the world: stops update ticks and pauses SFX sounds.

#### Resume()

```csharp
public virtual void Resume()
```

Resumes the world after a pause.

#### ActivateAllSystems()

```csharp
public void ActivateAllSystems()
```

Activates all systems that were previously deactivated.

#### DeactivateAllSystems(Type[])

```csharp
public void DeactivateAllSystems(Type[] skip)
```

Deactivates all systems except those whose types appear in the `skip` list.

**Parameters** \
`skip` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### Draw(RenderContext)

```csharp
public void Draw(RenderContext render)
```

Runs all active render systems for this frame.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \

#### DrawGui(RenderContext)

```csharp
public void DrawGui(RenderContext render)
```

Runs all active GUI render systems for this frame.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \

#### Exit()

```csharp
public void Exit()
```

Signals the world to exit; sets `IsExiting` to `true`.

#### FixedUpdate()

```csharp
public void FixedUpdate()
```

Runs all active fixed-update systems at the fixed timestep.

#### PreDraw()

```csharp
public void PreDraw()
```

Runs all active pre-render systems before the main draw pass.

#### RunCoroutine(IEnumerator&lt;Wait&gt;, CoroutineFlags)

```csharp
public Coroutine RunCoroutine(IEnumerator<Wait> routine, CoroutineFlags flags = CoroutineFlags.None)
```

Runs `routine` as a coroutine driven by a pooled, invisible entity's state machine, rather than requiring game code to create and manage its own entity. The routine's first tick runs immediately, synchronously, before this call returns. Prefer the `World.RunCoroutine` extension in `CoroutineServices` for call sites that only have an `ISystem`'s `World` reference; this method is what that extension ultimately calls into.

**Parameters** \
`routine` [IEnumerator\<Wait\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \
`flags` [CoroutineFlags](../../Murder/Services/CoroutineFlags.html) \

**Returns** \
[Coroutine](../../Murder/Core/Coroutine.html) \

#### Start()

```csharp
public void Start()
```

Calls the `Start` callback on all active start systems. Called once after the world is fully loaded.

#### Update()

```csharp
public void Update()
```

Runs all active update systems for the current frame.

⚡

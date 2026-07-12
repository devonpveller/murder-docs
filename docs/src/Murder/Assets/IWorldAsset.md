# IWorldAsset

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public abstract IWorldAsset
```

Common contract for any asset that stores a list of `EntityInstance`s and can populate a live `World` from them.

**Intent:** Provide a uniform API for loading and populating a Bang `World` from a stored set of entity instances, regardless of whether the source is a design-time level asset (`WorldAsset`) or a runtime save snapshot (`SavedWorld`), so world-loading code doesn't need to special-case either.

**Use-case:** Accept an `IWorldAsset` parameter in world-loading code so the same logic works for both initial `WorldAsset` loads and `SavedWorld` restores. Call `TryGetInstance` to retrieve individual entity data by GUID, enumerate `Instances` to iterate every entity GUID stored in the snapshot, or use the default `TryCreateEntityInWorld` implementation to spawn a single entity from this snapshot into a live world.

### ⭐ Properties

#### Instances

```csharp
public abstract virtual ImmutableArray<T> Instances { get; }
```

GUIDs of every entity instance stored in this world snapshot (not the instances themselves -- use `TryGetInstance` to resolve a GUID to its `EntityInstance` data). No particular ordering is guaranteed.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### WorldGuid

```csharp
public abstract virtual Guid WorldGuid { get; }
```

GUID that identifies which world this snapshot belongs to. For a `WorldAsset` this is its own `Guid`; a `SavedWorld` always returns `Guid.Empty` here since save snapshots are looked up by their own asset GUID rather than by `WorldGuid`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Methods

#### TryGetInstance(Guid)

```csharp
public abstract EntityInstance TryGetInstance(Guid instanceGuid)
```

Retrieves the `EntityInstance` with the given GUID from this snapshot; returns null if not found.

**Parameters** \
`instanceGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### TryCreateEntityInWorld(World, Guid)

```csharp
public virtual int TryCreateEntityInWorld(World world, Guid instance)
```

Default interface implementation that looks up the instance identified by `instance` via `TryGetInstance` and spawns it into `world`. Most callers use this rather than resolving the instance manually.

**Parameters** \
`world` [World](../../Bang/World.html) \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) -- the id of the newly created entity, or -1 if `instance` could not be found. \

⚡

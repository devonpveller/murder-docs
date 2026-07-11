# IWorldAsset

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public abstract IWorldAsset
```

Interface shared by all asset types that represent an instantiable world snapshot (e.g. `WorldAsset`, `SavedWorld`).

**Intent:** Provide a uniform API for loading and populating a Bang `World` from a stored list of `EntityInstance` objects, regardless of whether the source is a design-time level asset or a runtime save.

**Use-case:** Accept an `IWorldAsset` parameter in world-loading code so the same logic works for both initial `WorldAsset` loads and `SavedWorld` restores. Call `TryGetInstance` to retrieve individual entity data by GUID, or use `TryCreateEntityInWorld` to spawn a single entity from this snapshot.

### ⭐ Properties
#### Instances
```csharp
public abstract virtual ImmutableArray<T> Instances { get; }
```

Ordered list of all entity instances stored in this world snapshot.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### WorldGuid
```csharp
public abstract virtual Guid WorldGuid { get; }
```

The GUID that uniquely identifies this world (matching the corresponding `WorldAsset` GUID for saves).

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

Attempts to create a single entity from the stored `EntityInstance` with the given GUID into the live world; returns the entity ID or -1 on failure.

**Parameters** \
`world` [World](../../Bang/World.html) \
`instance` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
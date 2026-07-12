# WorldServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class WorldServices
```

Small set of extension utilities for querying Murder-specific metadata from a Bang `World` — the asset it was instantiated from, and mapping instance guids back to live entity ids.

**Intent:** Provides helpers that extract Murder-specific information from a generic `World` instance without every caller having to know about `MonoWorld` or the instance-lookup component internals.

**Use-case:** Call `Guid` to retrieve the `Guid` of the `WorldAsset` the current `World` was created from, useful for save-state tracking (e.g. `SaveData.CurrentWorld`) and scene comparison. Call `GuidToEntityId` to resolve an entity-instance guid (as authored in the world/prefab editor) back to the live runtime entity id, for example when a cutscene or save-file reference needs to find "the entity that was originally placed as instance X" in the currently running world.

### ⭐ Methods

#### Guid(World)

```csharp
public static Guid Guid(this World world)
```

Returns the `Guid` of the `WorldAsset` that the `MonoWorld` instance was created from (`((MonoWorld)world).WorldAssetGuid`). Assumes `world` is actually a `MonoWorld`; will throw an `InvalidCastException` if called on a bare Bang `World` that isn't Murder's `MonoWorld` subclass.

**Parameters** \
`world` [World](../../Bang/World.html) \

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### GuidToEntityId(World, Guid)

```csharp
public static int GuidToEntityId(World world, Guid guid)
```

Resolves an entity-instance `guid` (as assigned to instances placed in the world/prefab editor) to the live `EntityId` of that entity in `world`, using the world's unique `InstanceToEntityLookupComponent`. Returns `-1` if the lookup component is missing from the world, or if `guid` is not a known instance.

**Parameters** \
`world` [World](../../Bang/World.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

# InstanceToEntityLookupComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InstanceToEntityLookupComponent : IComponent
```

This is used when serializing save data. This keeps a reference between entities and their guid.

**Intent:** Maintain a bidirectional map between entity instance GUIDs (design-time identifiers) and their runtime integer entity IDs across save/load cycles.

**Use-case:** Attached to the world or a root entity during serialization; systems use `InstancesToEntities` to resolve a saved GUID back to a live entity, and `EntitiesToInstances` to go the other direction.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public InstanceToEntityLookupComponent()
```

Creates an empty lookup, with no known instance/entity mappings.

```csharp
public InstanceToEntityLookupComponent(IDictionary<Guid, int> instancesToEntities)
```

Creates a lookup from an explicit instance-guid-to-entity-id map, deriving the reverse `EntitiesToInstances` map automatically. Entries whose entity id is `-1` (i.e. the instance was never actually instantiated) are skipped when building the reverse map.

**Parameters** \
`instancesToEntities` [IDictionary\<Guid, int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IDictionary-2?view=net-7.0) \

### ⭐ Properties

#### EntitiesToInstances

```csharp
public readonly ImmutableDictionary<int, Guid> EntitiesToInstances;
```

This keeps a map of the entities (id) to their instances (guid) — the reverse of `InstancesToEntities`, derived automatically by the constructor.

**Returns** \
[ImmutableDictionary\<int, Guid\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### InstancesToEntities

```csharp
public readonly ImmutableDictionary<Guid, int> InstancesToEntities;
```

This keeps a map of the instances (guid) to their entities (id).

**Returns** \
[ImmutableDictionary\<Guid, int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

⚡

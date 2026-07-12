# GuidToIdTargetCollectionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct GuidToIdTargetCollectionComponent : IComponent
```

A design-time component used to translate entity instance GUIDs into actual runtime entity ids, for entities that need to reference several other entities by name. The `[Generates]` attribute tells the serialization pipeline that this component should be replaced with an `IdTargetCollectionComponent` (mapping each name to a live entity id) once the world is instantiated.

**Intent:** Persist multiple named GUID-to-entity mappings at design time so they can be resolved to runtime entity ids when the world is loaded, without the level author needing to know entity ids ahead of time (which don't exist until the world is instantiated).

**Use-case:** Add to an entity that needs to reference several other entities by name; `WorldProcessor.PostProcessEntitiesFirstTime` resolves each `GuidId` in `Collection` against the world's instance-to-entity map and replaces this component with an `IdTargetCollectionComponent` holding the resulting name-to-id dictionary.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public GuidToIdTargetCollectionComponent()
```

Creates a component with an empty collection of GUID references.

### ⭐ Properties

#### Collection

```csharp
public readonly ImmutableArray<GuidId> Collection;
```

The named GUID references authored for this entity; each entry maps a name to a target entity's instance GUID.

**Returns** \
[ImmutableArray\<GuidId\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### TryFindGuid(string)

```csharp
public Guid? TryFindGuid(string name)
```

Looks up the target GUID for the entry whose `Id` matches `name` (case-insensitive), or `null` if no entry with that name exists.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

⚡

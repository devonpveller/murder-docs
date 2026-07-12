# GuidToIdTargetComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct GuidToIdTargetComponent : IComponent
```

A design-time component used to translate a single entity instance GUID into an actual runtime entity id. `WorldProcessor.PostProcessEntitiesFirstTime` resolves `Target` against the world's instance-to-entity map and replaces this component with an [IdTargetComponent](../../Murder/Components/IdTargetComponent.html) holding the live entity id.

**Intent:** Store a single design-time GUID reference that is resolved to a runtime entity id when the world is instantiated, for cases where an entity needs to point at exactly one other entity (for several named references, use `GuidToIdTargetCollectionComponent` instead).

**Use-case:** Assign during level authoring to point one entity at another by GUID (e.g. a trigger pointing at the door it should open); the world-loading step automatically replaces it with an `IdTargetComponent` containing the resolved runtime entity id.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public GuidToIdTargetComponent(Guid target)
```

Creates a reference pointing at the entity with the given instance `target` GUID.

**Parameters** \
`target` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### Target

```csharp
public readonly Guid Target;
```

The design-time instance GUID of the referenced entity, resolved to a runtime entity id on world load.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡

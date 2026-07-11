# GuidToIdTargetComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct GuidToIdTargetComponent : IComponent
```

This is a component used to translate entity instaces guid to an actual entity id.
            Gets translated to [IdTargetComponent](../../Murder/Components/IdTargetComponent.html).

**Intent:** Store a single design-time GUID reference that is resolved to a runtime entity ID when the world is instantiated.

**Use-case:** Assign during level authoring to point one entity at another by GUID; the serialization system automatically replaces it with an `IdTargetComponent` containing the live entity ID.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public GuidToIdTargetComponent(Guid target)
```

**Parameters** \
`target` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### Target
```csharp
public readonly Guid Target;
```

Guid of the target entity.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \


⚡
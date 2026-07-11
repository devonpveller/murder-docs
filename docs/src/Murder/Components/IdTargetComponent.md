# IdTargetComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct IdTargetComponent : IComponent
```

This is a component used to track other entities when triggering an interaction or other
            action.

**Intent:** Store a runtime reference to a single target entity by its integer ID for use by interaction and trigger systems.

**Use-case:** Attached by the serialization system after resolving `GuidToIdTargetComponent`; read `Target` to obtain the live entity ID to interact with or follow.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public IdTargetComponent(int target)
```

**Parameters** \
`target` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Target
```csharp
public readonly int Target;
```

Id of the target entity.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
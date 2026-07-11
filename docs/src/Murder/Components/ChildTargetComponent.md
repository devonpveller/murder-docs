# ChildTargetComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct ChildTargetComponent : IComponent
```

Identifies a named child entity that other systems should target or interact with.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Stores the name of a child entity so parent-level systems can resolve the correct child without hard-coding entity IDs.

**Use-case:** Attach to a parent entity and set `Name` to the child entity's identifier; interaction and event systems use this to route actions to the correct child.

### ⭐ Constructors
```csharp
public ChildTargetComponent()
```

### ⭐ Properties
#### Name
```csharp
public readonly string Name;
```

Name of the target child entity, as assigned in the entity hierarchy.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡
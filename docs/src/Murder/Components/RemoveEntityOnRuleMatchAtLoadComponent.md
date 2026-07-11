# RemoveEntityOnRuleMatchAtLoadComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RemoveEntityOnRuleMatchAtLoadComponent : IComponent
```

This will remove the entity that contains this component as soon as the entity is serialized
            into an actual world instance.

**Intent:** Conditionally eliminate an entity from the world at load time based on blackboard state.

**Use-case:** Attach to optional world entities (e.g. a chest that has already been looted) so they are removed automatically when the scene loads if the relevant save-state conditions are met.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public RemoveEntityOnRuleMatchAtLoadComponent()
```

### ⭐ Properties
#### Requirements
```csharp
public readonly ImmutableArray<T> Requirements;
```

List of requirements which will trigger the interactive component within the same entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
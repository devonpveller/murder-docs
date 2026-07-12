# RemoveEntityOnRuleMatchAtLoadComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RemoveEntityOnRuleMatchAtLoadComponent : IComponent
```

One-shot conditional removal: as soon as this component is added to an entity (which normally happens right when the entity is instantiated into a live world), `RemoveEntityOnRuleMatchAtLoadSystem` evaluates `Requirements` against the current save's blackboard and, if they match, destroys the entity.

**Intent:** Conditionally eliminate an entity from the world at load time based on saved blackboard state.

**Use-case:** Attach to optional world entities (e.g. a chest that has already been looted, or a one-time cutscene trigger) so they are removed automatically when the scene loads if the relevant save-state conditions are already met. If the entity also has an `IdTargetComponent` pointing at another entity, that target entity is destroyed as well. Either way, the component removes itself right after being checked, so the evaluation only ever runs once.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public RemoveEntityOnRuleMatchAtLoadComponent()
```

Creates a component with an empty requirement list. Because the system requires at least one requirement to match, an empty list never matches — this constructor form is effectively inert (the entity survives). Use a collection initializer with an explicit `Requirements` list to actually condition removal on blackboard state.

### ⭐ Properties

#### Requirements

```csharp
public readonly ImmutableArray<CriterionNode> Requirements;
```

Blackboard requirements which, when all satisfied, cause the owning entity (and its `IdTarget`, if any) to be destroyed the first time this component is processed.

**Returns** \
[ImmutableArray\<CriterionNode\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

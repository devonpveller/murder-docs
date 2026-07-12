# RequirementsCollection

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public readonly struct RequirementsCollection
```

A single set of blackboard/story criteria that gates one way of starting a `TriggerEventOn`.

**Intent:** Wraps a list of `CriterionNode` conditions (blackboard facts, story flags, weights, etc.) that must all match for this particular requirement set to be considered satisfied. It is not, despite the generic name, a collection of required *components* — it's a collection of *narrative/blackboard criteria*, matched via `BlackboardHelpers.Match`.

**Use-case:** A `TriggerEventOn` can carry several `RequirementsCollection` values in its `Requirements` array; each one becomes its own independent `InteractOnRuleMatchComponent` rule when `TriggerEventOn.CreateComponents` runs, so the trigger fires the moment *any one* of the alternative requirement sets is satisfied (an "OR of ANDs" match). Use multiple `RequirementsCollection` entries to express "start this trigger if condition set A matches, OR if condition set B matches".

### ⭐ Constructors

```csharp
public RequirementsCollection()
```

Creates an empty requirements collection with no requirements. Used by the editor/serializer as the blank starting state.

### ⭐ Properties

#### Requirements

```csharp
public readonly ImmutableArray<CriterionNode> Requirements;
```

List of requirements which will trigger the interactive component within the same entity.

**Returns** \
[ImmutableArray\<CriterionNode\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

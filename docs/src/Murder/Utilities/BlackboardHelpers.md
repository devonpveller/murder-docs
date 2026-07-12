# BlackboardHelpers

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static partial class BlackboardHelpers
```

Static helpers for evaluating blackboard-driven rule sets (used by narrative/interaction requirements) against the active save's `BlackboardTracker`, and for interpolating blackboard variables into dialogue/UI text.

**Intent:** Provides the shared "is this allowed to happen right now" evaluation logic that requirement/condition-bearing components (dialogue options, interaction rules, cutscene triggers) route through, so criterion matching and text formatting behave consistently across every system that uses them.

**Use-case:** Call `Match` to test story/blackboard conditions, `IsSatisfied`/`IsAnySatisfied` to evaluate world or entity conditions, and `FormatText` to interpolate blackboard variable values into dialogue strings.

### ⭐ Methods

#### FormatText(string, FormatTextFlags, out String&)

```csharp
public bool FormatText(string text, FormatTextFlags flags, String& newText)
```

Replaces `{fieldName}` placeholders in `text` with their current values from the active save's `BlackboardTracker`; sets `newText` to the result and returns `true` if any substitution was made. Pass `FormatTextFlags.Cache` to reuse (and populate) the tracker's formatted-text cache instead of always re-running the substitution — useful for static dialogue lines that are re-rendered every frame.

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`flags` [FormatTextFlags](../../Murder/Utilities/BlackboardHelpers.FormatTextFlags.html) \
`newText` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsAnySatisfied(World, ImmutableArray<T>)

```csharp
public bool IsAnySatisfied(World world, ImmutableArray<T> conditions)
```

OR counterpart to `IsSatisfied(World, ImmutableArray<ICondition>)`: returns `true` if `conditions` is empty or if at least one condition in it is satisfied for `world`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`conditions` [ImmutableArray\<ICondition\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsSatisfied(World, Entity, ImmutableArray<T>)

```csharp
public bool IsSatisfied(World world, Entity target, ImmutableArray<T> conditions)
```

Returns `true` only if every condition in `conditions` is satisfied by `target` (an empty array trivially passes). Used for entity-scoped conditions, e.g. "this specific NPC must be alive," as opposed to the world-scoped overload below.

**Parameters** \
`world` [World](../../Bang/World.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \
`conditions` [ImmutableArray\<IEntityCondition\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsSatisfied(World, ImmutableArray<T>)

```csharp
public bool IsSatisfied(World world, ImmutableArray<T> conditions)
```

Returns `true` only if every condition in `conditions` is satisfied for `world` as a whole (an empty array trivially passes). Use for global/world-scoped gating rather than a specific entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`conditions` [ImmutableArray\<ICondition\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Match(World, BlackboardTracker, ImmutableArray<T>)

```csharp
public bool Match(World world, BlackboardTracker tracker, ImmutableArray<T> requirements)
```

Evaluates an ordered list of `CriterionNode` requirements against `tracker`, respecting each node's AND/OR join with the *next* node: it short-circuits to `false` as soon as a node fails and the following node is AND-joined, and otherwise returns whether at least one node matched by the end (so a trailing run of OR nodes only needs a single hit to pass).

**Parameters** \
`world` [World](../../Bang/World.html) \
`tracker` [BlackboardTracker](../../Murder/Save/BlackboardTracker.html) \
`requirements` [ImmutableArray\<CriterionNode\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Match(World, Entity, OnlyApplyOnRuleComponent)

```csharp
public bool Match(World world, Entity target, OnlyApplyOnRuleComponent onlyApplyWhen)
```

Composite check combining an `OnlyApplyOnRuleComponent`'s entity conditions, blackboard requirements, and world conditions into a single pass/fail result. This is the entry point most gameplay code should call when deciding whether an `OnlyApplyOnRuleComponent`-gated effect is currently allowed to trigger; `target` may be `null` if the rule has no entity-scoped conditions.

**Parameters** \
`world` [World](../../Bang/World.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \
`onlyApplyWhen` [OnlyApplyOnRuleComponent](../../Murder/Components/OnlyApplyOnRuleComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Match(World, ImmutableArray<T>)

```csharp
public bool Match(World world, ImmutableArray<T> requirements)
```

Fetches the active save's `BlackboardTracker` and evaluates the criterion nodes; returns `true` if `requirements` is empty, `false` if there is no active save, and otherwise the result of `Match(World, BlackboardTracker, ImmutableArray<CriterionNode>)`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`requirements` [ImmutableArray\<CriterionNode\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Nested Types

#### FormatTextFlags

```csharp
[Flags]
public enum FormatTextFlags
```

Flags controlling how `FormatText` resolves blackboard-variable placeholders: `None` always re-resolves from the current blackboard state; `Cache` reads from (and writes to) the tracker's formatted-text cache instead.

⚡

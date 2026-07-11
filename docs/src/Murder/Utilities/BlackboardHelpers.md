# BlackboardHelpers

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class BlackboardHelpers
```

Static helpers for evaluating blackboard rule sets against the current save state and for formatting blackboard-variable placeholders in text strings.

**Intent:** Provides the core matching logic used by rule-driven systems to check whether a set of `CriterionNode` conditions is satisfied.

**Use-case:** Call `Match` to test story conditions, or `FormatText` to interpolate blackboard variable values into dialogue strings.

### ⭐ Methods
#### FormatText(string, out String&)
```csharp
public bool FormatText(string text, String& newText)
```

Replaces blackboard-variable placeholders in `text` with their current values; sets `newText` to the result and returns `true` if any substitution was made.

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`newText` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Match(World, BlackboardTracker, ImmutableArray<T>)
```csharp
public bool Match(World world, BlackboardTracker tracker, ImmutableArray<T> requirements)
```

Evaluates the criterion nodes against the given `tracker` and returns `true` if the requirements are satisfied (respecting AND/OR logic).

**Parameters** \
`world` [World](../../Bang/World.html) \
`tracker` [BlackboardTracker](../../Murder/Save/BlackboardTracker.html) \
`requirements` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Match(World, ImmutableArray<T>)
```csharp
public bool Match(World world, ImmutableArray<T> requirements)
```

Fetches the active save's `BlackboardTracker` and evaluates the criterion nodes; returns `true` if all requirements are met.

**Parameters** \
`world` [World](../../Bang/World.html) \
`requirements` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \



⚡
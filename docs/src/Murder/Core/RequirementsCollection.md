# RequirementsCollection

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct RequirementsCollection
```

An immutable collection of component-type requirements that must be satisfied before an interaction or rule fires.

**Intent:** Groups a set of required component types so rule-based systems can gate interactions on entity state.

**Use-case:** Add to an entity alongside an interaction component; the engine checks `Requirements` before evaluating the interaction so it only triggers when all listed components are present.

### ⭐ Constructors
```csharp
public RequirementsCollection()
```

Creates an empty requirements collection with no requirements.

### ⭐ Properties
#### Requirements
```csharp
public readonly ImmutableArray<T> Requirements;
```

List of requirements which will trigger the interactive component within the same entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
# TargetedInteractionCollectionItem

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct TargetedInteractionCollectionItem
```

Pairs a named target identifier with a list of interactions to run against the resolved entity.

**Intent:** Defines a single (target, interactions) binding inside a [TargetedInteractionCollection](../../Murder/Interactions/TargetedInteractionCollection.html).

**Use-case:** Configure one entry per distinct entity you wish to interact with; set `Target` to the name key in the `IdTargetCollection` and populate `InteractionCollection` with the desired actions.

### ⭐ Constructors
```csharp
public TargetedInteractionCollectionItem()
```

### ⭐ Properties
#### InteractionCollection
```csharp
public readonly ImmutableArray<T> InteractionCollection;
```
The interactions to fire against the resolved target entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Target
```csharp
public readonly string Target;
```
The name key used to look up the target entity in the `IdTargetCollection` of the interacted entity.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡
# TargetedInteractionCollectionItem

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct TargetedInteractionCollectionItem
```

Pairs a named target identifier with a list of interactions to run against the resolved entity.

**Intent:** Defines a single (target, interactions) binding inside a [TargetedInteractionCollection](../../Murder/Interactions/TargetedInteractionCollection.html).

**Use-case:** Configure one entry per distinct entity you wish to interact with: set `Target` to the name key registered in the interacted entity's `IdTargetCollectionComponent`, and populate `InteractionCollection` with the interactions that should run against the resolved entity.

### ⭐ Constructors

```csharp
public TargetedInteractionCollectionItem()
```

### ⭐ Properties

#### InteractionCollection

```csharp
public readonly ImmutableArray<T> InteractionCollection;
```

The interactions ([IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) instances) to fire against the entity resolved from `Target` — or against `null` if `Target` does not resolve to an entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Target

```csharp
public readonly string Target;
```

The name key used to look up the target entity in the interacted entity's `IdTargetCollectionComponent`. If the name does not resolve to an entity, `InteractionCollection` still runs, but with a `null` target.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

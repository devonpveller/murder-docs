# IdTargetCollectionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct IdTargetCollectionComponent : IComponent
```

This is a component with a collection of entities tracked in the world.

**Intent:** Store a named set of runtime entity ID references so that systems can look up multiple target entities by string key.

**Use-case:** Attached by the serialization system after resolving `GuidToIdTargetCollectionComponent`; read `Targets` to find the live entity IDs associated with each named reference.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public IdTargetCollectionComponent(ImmutableDictionary<TKey, TValue> targets)
```

**Parameters** \
`targets` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

### ⭐ Properties
#### Targets
```csharp
public readonly ImmutableDictionary<TKey, TValue> Targets;
```

Id of the target entity.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \


⚡
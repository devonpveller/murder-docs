# MurderTargetedRuntimeAction

**Namespace:** Murder.Core.MurderActions \
**Assembly:** Murder.dll

```csharp
public sealed struct MurderTargetedRuntimeAction
```

Runtime counterpart of `MurderTargetedAction` where the target has been resolved to a concrete entity ID.

**Intent:** Stores a live entity ID alongside its interaction list so the interaction system can execute actions without a second GUID-to-entity lookup.

**Use-case:** Created by the interaction system after resolving `MurderTargetedAction.Target` to an entity ID; consumed each frame by interaction processing systems.

### ⭐ Constructors
```csharp
public MurderTargetedRuntimeAction(int id, ImmutableArray<T> interaction)
```

Creates a runtime action targeting the entity with the given `id` and the specified `interaction` list.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`interaction` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### EntityId
```csharp
public readonly int EntityId;
```

The runtime integer ID of the target entity that the interactions will be applied to.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Interaction
```csharp
public readonly ImmutableArray<T> Interaction;
```

The ordered list of interactions to execute against the target entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
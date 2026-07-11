# BlackboardAction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct BlackboardAction
```

A conditional action bundle that checks a set of blackboard criteria, then applies dialog actions and fires interactions when the criteria are met.

**Intent:** Encapsulates a guarded set of blackboard mutations and sub-interactions that only execute when all required criteria pass.

**Use-case:** Use inside [AdvancedBlackboardInteraction](../../Murder/Interactions/AdvancedBlackboardInteraction.html) to create branching behaviour where different sets of consequences fire depending on the current game state.

### ⭐ Constructors
```csharp
public BlackboardAction()
```

### ⭐ Properties
#### _interactions
```csharp
public readonly ImmutableArray<T> _interactions;
```
The list of interactions to fire when all criteria are satisfied.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### Invoke(World, Entity, Entity)
```csharp
public void Invoke(World world, Entity interactor, Entity interacted)
```
Evaluates requirements against the active blackboard and, if they pass, applies dialog actions and fires all configured interactions.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
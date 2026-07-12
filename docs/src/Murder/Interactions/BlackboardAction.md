# BlackboardAction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct BlackboardAction
```

A single guarded bundle of consequences: a list of blackboard criteria that must all match, plus the dialog actions and sub-interactions to run when they do.

**Intent:** Encapsulates a guarded set of blackboard mutations and sub-interactions that only execute when all required criteria pass.

**Use-case:** Used as the building block of [AdvancedBlackboardInteraction](../../Murder/Interactions/AdvancedBlackboardInteraction.html), where several of these bundles are evaluated in sequence so different sets of consequences fire depending on the current save/blackboard state — similar to a dialog line's conditional actions, but driven from a world interaction instead of dialogue.

### ⭐ Constructors

```csharp
public BlackboardAction()
```

### ⭐ Properties

#### \_interactions

```csharp
public readonly ImmutableArray<IInteractiveComponent> _interactions;
```

The interactions fired, in order, once the requirements are satisfied and the configured dialog actions have been applied. This lets a single conditional bundle both mutate the blackboard and trigger arbitrary side-effects (spawn an entity, play a sound, etc.) in one step.

**Returns** \
[ImmutableArray\<IInteractiveComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### Invoke(World, Entity, Entity)

```csharp
public void Invoke(World world, Entity interactor, Entity interacted)
```

Evaluates the configured requirements against the active save's blackboard; if they all pass, applies the configured dialog actions to the blackboard and then invokes every entry in `_interactions`. If the bundle is configured to trigger only once, the interacted entity is destroyed afterwards so it cannot run again.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡

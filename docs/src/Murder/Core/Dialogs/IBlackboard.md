# IBlackboard

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public abstract IBlackboard
```

This is a blackboard tracker with dialogue variables.
            This is used when defining the set of conditions which will play a given dialog.

**Intent:** Defines the contract for any blackboard implementation — a key-value store of typed dialogue variables that drive conditional dialogue logic.

**Use-case:** Implement this interface (or extend `ICharacterBlackboard` / `ISoundBlackboard`) to create a custom blackboard class, annotate it with `[Blackboard]`, and expose public fields for every fact the dialogue system should be able to read or write.

### ⭐ Properties
#### Kind
```csharp
public virtual BlackboardKind Kind { get; }
```

Identifies which blackboard scope this instance belongs to; defaults to `BlackboardKind.Gameplay`.

**Returns** \
[BlackboardKind](../../../Murder/Core/Dialogs/BlackboardKind.html) \


⚡
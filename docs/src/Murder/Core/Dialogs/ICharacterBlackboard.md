# ICharacterBlackboard

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public abstract class ICharacterBlackboard : IBlackboard
```

This works similarly as a [IBlackboard](../../../Murder/Core/Dialogs/IBlackboard.html), except that each situation
            on the game has its own table.

**Intent:** Marks a blackboard as character-scoped, ensuring the engine tracks its state per-character rather than globally.

**Use-case:** Extend this class instead of `IBlackboard` when your custom blackboard should hold data that is specific to a single NPC's dialogue history (e.g. how many times a particular topic was discussed).

**Implements:** _[IBlackboard](../../../Murder/Core/Dialogs/IBlackboard.html)_

### ⭐ Constructors
```csharp
protected ICharacterBlackboard()
```

Protected constructor for subclasses.

### ⭐ Properties
#### Kind
```csharp
public virtual BlackboardKind Kind { get; }
```

Always returns `BlackboardKind.Character` for character-scoped blackboards.

**Returns** \
[BlackboardKind](../../../Murder/Core/Dialogs/BlackboardKind.html) \


⚡
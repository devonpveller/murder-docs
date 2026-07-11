# BaseCharacterBlackboard

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public class BaseCharacterBlackboard : ICharacterBlackboard, IBlackboard
```

Built-in capabilities for each speaker blackboard.

**Intent:** Provides the default blackboard implementation shared by all dialogue speakers, tracking built-in per-character state such as total interaction counts.

**Use-case:** Inherit from this class when creating a custom character blackboard so you automatically get standard character facts (e.g. `TotalInteractions`) alongside your own fields.

**Implements:** _[ICharacterBlackboard](../../../Murder/Core/Dialogs/ICharacterBlackboard.html), [IBlackboard](../../../Murder/Core/Dialogs/IBlackboard.html)_

### ⭐ Constructors
```csharp
public BaseCharacterBlackboard()
```

Initializes a new instance of the base character blackboard with default values.

### ⭐ Properties
#### Kind
```csharp
public virtual BlackboardKind Kind { get; }
```

Returns `BlackboardKind.Character`, indicating this blackboard tracks per-character dialogue state.

**Returns** \
[BlackboardKind](../../../Murder/Core/Dialogs/BlackboardKind.html) \
#### Name
```csharp
public static const string Name;
```

The registered blackboard name (`"Character"`), used to look up this blackboard type in the engine.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### TotalInteractions
```csharp
public int TotalInteractions;
```

Total of times that it has been interacted to.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
# SoundRuleAction

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundRuleAction
```

This is a generic blackboard action with a command.

**Intent:** Represent a rule action that writes a value to a `SoundFact` on the audio blackboard.

**Use-case:** Use `SoundRuleAction` in sound rule assets to update blackboard facts when game events occur (e.g. marking a music zone as entered), so the adaptive audio system can react.

### ⭐ Constructors
```csharp
public SoundRuleAction()
```

```csharp
public SoundRuleAction(SoundFact fact, BlackboardActionKind kind, T? value)
```

**Parameters** \
`fact` [SoundFact](../../../Murder/Core/Sounds/SoundFact.html) \
`kind` [BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
`value` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

### ⭐ Properties
#### Fact
```csharp
public readonly SoundFact Fact;
```

The audio blackboard fact this action targets.

**Returns** \
[SoundFact](../../../Murder/Core/Sounds/SoundFact.html) \
#### Kind
```csharp
public readonly BlackboardActionKind Kind;
```

The operation to apply to the fact (Set, Add, etc.).

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
#### Value
```csharp
public readonly T? Value;
```

The integer value applied to the fact according to `Kind`; `null` means no value change.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \


⚡
# ParameterRuleAction

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct ParameterRuleAction
```

This is a generic blackboard action with a command.

**Intent:** Represent an adaptive audio rule that modifies a `ParameterId` value when triggered.

**Use-case:** Use `ParameterRuleAction` in dialogue or world event rules to set or increment an FMOD parameter at specific moments, enabling adaptive music and sound responses.

### ⭐ Constructors
```csharp
public ParameterRuleAction()
```

```csharp
public ParameterRuleAction(ParameterId parameter, BlackboardActionKind kind, float value)
```

**Parameters** \
`parameter` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \
`kind` [BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Kind
```csharp
public readonly BlackboardActionKind Kind;
```

The operation to apply to the parameter (Set, Add, etc.).

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
#### Parameter
```csharp
public readonly ParameterId Parameter;
```

The audio parameter this action targets.

**Returns** \
[ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \
#### Value
```csharp
public readonly float Value;
```

The value applied to the parameter according to `Kind`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡
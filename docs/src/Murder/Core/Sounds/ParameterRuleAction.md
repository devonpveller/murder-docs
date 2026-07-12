# ParameterRuleAction

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct ParameterRuleAction
```

This is a generic blackboard action with a command.

**Intent:** Represent a single "write this value to this FMOD parameter" step, bypassing the blackboard entirely and going straight to the audio middleware.

**Use-case:** `SetSoundParameterOnInteraction` carries an `ImmutableArray<ParameterRuleAction>` (`MiddlewareParameterTriggers`) that is applied whenever the interaction fires. Unlike `SoundRuleAction`, whose value lands in the save's blackboard, a `ParameterRuleAction` writes directly to FMOD via `SoundServices.SetGlobalParameter`; `Kind` of `Add`/`Minus` first reads the parameter's current value with `SoundServices.GetGlobalParameter` and applies the delta, while any other `Kind` performs an absolute `Set`. This is the mechanism for things like nudging a "tension" or "combat" parameter from a trigger volume or scripted event without round-tripping through blackboard facts.

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

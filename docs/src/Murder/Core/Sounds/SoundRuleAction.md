# SoundRuleAction

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundRuleAction
```

This is a generic blackboard action with a command.

**Intent:** Represent a single "write this value to this blackboard fact" step, driven by sound-related gameplay events rather than dialogue.

**Use-case:** `SetSoundParameterOnInteraction` carries an `ImmutableArray<SoundRuleAction>` (`BlackboardTriggers`) that is applied whenever the interaction fires (e.g. an animation event, a trigger volume, an explicit call from gameplay code). For each action, `Kind` chooses between an absolute `Set` (writes `Value` via `BlackboardTracker.SetValue`) or a relative `Add`/`Minus` (adjusts the fact via `BlackboardTracker.SetInt`). This lets a level designer wire "entering this trigger sets `music_intensity` to 2" or "this pickup adds 1 to `collectibles_found`" without writing code — the editor's `SoundRuleActionComponent`/`SoundFactField` provide the picker UI for `Fact`, `Kind`, and `Value`.

### ⭐ Constructors

```csharp
public SoundRuleAction()
```

Default constructor; produces an action with an empty `Fact`, `Kind` set to `Set`, and `Value` set to `null`, which the editor then fills in field-by-field.

```csharp
[JsonConstructor]
public SoundRuleAction(SoundFact fact, BlackboardActionKind kind, int? value)
```

The `[JsonConstructor]`-attributed constructor used by the serializer (and by code that builds a `SoundRuleAction` directly) to set all three fields at once.

**Parameters** \
`fact` [SoundFact](../../../Murder/Core/Sounds/SoundFact.html) \
`kind` [BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
`value` [int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

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
public readonly int? Value;
```

The integer value applied to the fact according to `Kind`. If `null`, `SetSoundParameterOnInteraction` logs an error and skips the action instead of writing to the blackboard.

**Returns** \
[int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

⚡

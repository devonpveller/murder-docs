# QuestStage

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct QuestStage
```

Defines a single stage within a quest, including its activation requirements and the actions to execute when those requirements are met.

**Intent:** Describe one step of a multi-stage quest: the conditions that unlock it and the gameplay actions it triggers.

**Use-case:** Build an array of `QuestStage` values and store them in a [QuestTrackerComponent](../../Murder/Components/QuestTrackerComponent.html) to describe the full quest progression.

### ⭐ Constructors
```csharp
public QuestStage()
```

### ⭐ Properties
#### Actions
```csharp
public readonly ImmutableArray<T> Actions;
```

Interaction actions executed when all requirements for this stage are satisfied.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Commentary
```csharp
public readonly string Commentary;
```

Optional designer note or description that explains the intent of this quest stage.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Requirements
```csharp
public readonly ImmutableArray<T> Requirements;
```

Blackboard criteria that must all be true before this stage becomes active.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
# QuestStageRuntime

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct QuestStageRuntime
```

Runtime representation of a single quest stage, holding the evaluated requirements and pending actions for the current session.

**Intent:** Cache the evaluated state of a [QuestStage](../../Murder/Components/QuestStage.html) so it can be checked and advanced each frame without re-reading the asset.

**Use-case:** Created automatically from [QuestTrackerComponent](../../Murder/Components/QuestTrackerComponent.html) data at runtime and stored in [QuestTrackerRuntimeComponent](../../Murder/Components/QuestTrackerRuntimeComponent.html).

### ⭐ Constructors
```csharp
public QuestStageRuntime()
```

```csharp
public QuestStageRuntime(ImmutableArray<T> requirements, ImmutableArray<T> actions)
```

**Parameters** \
`requirements` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`actions` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### Actions
```csharp
public readonly ImmutableArray<T> Actions;
```

Pending actions for this stage that will be executed when requirements are met.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Requirements
```csharp
public readonly ImmutableArray<T> Requirements;
```

Current runtime state of each requirement criterion for this quest stage.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
# QuestTrackerRuntimeComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct QuestTrackerRuntimeComponent : IComponent
```

Runtime counterpart of [QuestTrackerComponent](../../Murder/Components/QuestTrackerComponent.html) that holds the live evaluation state for each quest stage during a play session.

**Intent:** Track which quest stages have been completed and which are still pending at runtime.

**Use-case:** Read or modify this component in systems that need to respond to quest progression events; it is created automatically from [QuestTrackerComponent](../../Murder/Components/QuestTrackerComponent.html) at world load.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public QuestTrackerRuntimeComponent()
```

```csharp
public QuestTrackerRuntimeComponent(ImmutableArray<T> questStages)
```

**Parameters** \
`questStages` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### QuestStages
```csharp
public readonly ImmutableArray<T> QuestStages;
```

Current runtime state of every stage in the quest.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
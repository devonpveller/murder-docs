# QuestTrackerComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct QuestTrackerComponent : IComponent
```

Describes a quest as an ordered list of stages, each with its own requirements and actions. This is the design-time definition that is baked into the entity.

**Intent:** Attach quest progression data to an entity so the engine can track and advance it at runtime.

**Use-case:** Add to a quest-giver entity or a global manager entity; the engine converts it to [QuestTrackerRuntimeComponent](../../Murder/Components/QuestTrackerRuntimeComponent.html) at load time and updates it each tick.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public QuestTrackerComponent()
```

### ⭐ Properties
#### Name
```csharp
public readonly string Name;
```

Human-readable identifier for this quest, used for logging and editor display.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### QuestStages
```csharp
public readonly ImmutableArray<T> QuestStages;
```

Ordered list of stages that make up this quest.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡
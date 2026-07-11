# QuestTrackerSystem

**Namespace:** Murder.Systems.Utilities \
**Assembly:** Murder.dll

```csharp
public class QuestTrackerSystem : IReactiveSystem, ISystem
```

Reacts to quest-related component changes and updates quest state based on blackboard conditions.

**Intent:** Updates quest progress when quest-tracker components are added or modified.

**Use-case:** Include in worlds that use Murder's quest and blackboard system to automatically progress quests when conditions are met.

**Implements:** _[IReactiveSystem](../../../Bang/Systems/IReactiveSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public QuestTrackerSystem()
```

### ⭐ Methods
#### OnAdded(World, ImmutableArray<T>)
```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)
```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)
```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \



⚡
# InteractOnRuleMatchSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class InteractOnRuleMatchSystem : IStartupSystem, ISystem, IReactiveSystem
```

Watches for changes to `RuleWatcherComponent` and fires interaction events on entities whose `InteractOnRuleMatchComponent` conditions are satisfied by the current blackboard state.

**Intent:** Triggers interactions reactively whenever blackboard variables satisfy the rule conditions defined on an entity.

**Use-case:** Use with dialogue or game-state flags to make objects react automatically when story conditions are met, without needing to poll the blackboard each frame.

**Implements:** _[IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)_

### ⭐ Constructors

```csharp
public InteractOnRuleMatchSystem()
```

### ⭐ Methods

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Triggered when the `RuleWatcherComponent` is first added; runs an initial rule evaluation pass against the current blackboard state.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Re-evaluates all `InteractOnRuleMatchComponent` entities against current blackboard state and fires interaction events for any newly matched rules.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Clears the `RuleMatched` component from entities that were previously marked as having a matched rule.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Start(Context)

```csharp
public virtual void Start(Context context)
```

Adds the singleton `RuleWatcherComponent` entity to the world that reactive rule checks depend on.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡

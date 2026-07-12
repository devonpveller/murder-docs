# RuleWatcherComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RuleWatcherComponent : IModifiableComponent, IComponent
```

This will watch for rule changes based on the blackboard system.

**Intent:** An [IModifiableComponent](../../Bang/Components/IModifiableComponent.html) that bridges Bang's entity-modified notifications to the save system's `BlackboardTracker`. It carries no data of its own — its whole purpose is to make an entity "look modified" to Bang (and thus re-run any `[Watch]`-filtered system on it) any time a `Gameplay` or `Story` blackboard fact changes, without any game code having to manually replace the component.

**Use-case:** `InteractOnRuleMatchSystem` adds a single `RuleWatcherComponent` entity at startup (`context.World.AddEntity(new RuleWatcherComponent())`); it, `PlayAnimationOnRuleMatchSystem`, and `DestroyOnBlackboardConditionSystem` all declare `[Filter(typeof(RuleWatcherComponent))]` + `[Watch(typeof(RuleWatcherComponent))]`, so their `OnModified` callback fires automatically whenever any `Gameplay` or `Story` blackboard variable is written, letting them re-evaluate rule-based interactions, animations, and destroy conditions in reaction to story progress. Marked `[Unique]` (only one instance should exist in the world), `[RuntimeOnly]`, and `[DoNotPersistEntityOnSave]`, since it is pure wiring and must never be saved.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Methods

#### Subscribe(Action)

```csharp
public virtual void Subscribe(Action notification)
```

Registers a callback that fires whenever gameplay or story blackboard values change.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)

```csharp
public virtual void Unsubscribe(Action notification)
```

Removes a previously registered blackboard-change callback.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

⚡

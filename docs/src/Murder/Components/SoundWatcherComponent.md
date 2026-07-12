# SoundWatcherComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundWatcherComponent : IModifiableComponent, IComponent
```

This will watch for rule changes based on the blackboard system.

**Intent:** The `Sound`-blackboard sibling of [RuleWatcherComponent](../../Murder/Components/RuleWatcherComponent.html): an [IModifiableComponent](../../Bang/Components/IModifiableComponent.html) that carries no data of its own and exists purely so Bang treats its owning entity as "modified" whenever a `BlackboardKind.Sound` fact changes, letting any `[Watch(typeof(SoundWatcherComponent))]` system react without the component ever being replaced by hand.

**Use-case:** No system in the engine currently adds or watches this component — unlike [RuleWatcherComponent](../../Murder/Components/RuleWatcherComponent.html) (wired up by `InteractOnRuleMatchSystem`), `SoundWatcherComponent` ships as a ready-made extension point. A game that needs to react specifically to `BlackboardKind.Sound` changes (e.g. driving music/ambience layers off sound-related flags without also waking up on every `Gameplay`/`Story` write) can add one entity carrying this component and put `[Filter(typeof(SoundWatcherComponent))]` + `[Watch(typeof(SoundWatcherComponent))]` on a custom `IReactiveSystem`. Marked `[Unique]`, `[RuntimeOnly]`, and `[DoNotPersistEntityOnSave]` since it is pure wiring and must never be saved.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Methods

#### Subscribe(Action)

```csharp
public virtual void Subscribe(Action notification)
```

Registers a callback that fires whenever the sound blackboard values change.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)

```csharp
public virtual void Unsubscribe(Action notification)
```

Removes a previously registered sound-blackboard-change callback.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

⚡

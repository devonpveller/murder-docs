# TriggerEventOn

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public readonly struct TriggerEventOn
```

Declarative, authoring-time description of a named trigger event: what condition(s) must hold for it to fire, which interactions it runs when it does, and (optionally) which world it applies to.

**Intent:** Unlike `InteractOnRuleMatchComponent`, which is a runtime ECS component, `TriggerEventOn` is a plain data value used by assets/actions to describe a trigger declaratively. Call `CreateComponents` to convert it into the actual `IComponent`s (`InteractOnStartComponent`, `InteractOnRuleMatchCollectionComponent`, `InteractiveComponent<InteractionCollection>`) that get attached to an entity to make the trigger live.

**Use-case:** Build a `TriggerEventOn` when defining a scripted event (a cutscene beat, a story flag payoff, an environmental trigger) with a name, a list of `RequirementsCollection` blackboard conditions, and a list of `Triggers` (interactions) to run once those conditions match. Then call `CreateComponents()` and add the resulting components to the entity that should own the trigger.

### ⭐ Constructors

```csharp
public TriggerEventOn()
```

Creates an empty, unnamed trigger with no requirements and no targets. Used by the editor/serializer as the blank starting state.

```csharp
public TriggerEventOn(string name)
```

Creates a trigger with the given display name and everything else left at its default (fires immediately, no targets).

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Name

```csharp
public readonly string Name;
```

The display/identifying name of this trigger event, mainly for editor/authoring purposes.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Properties

```csharp
public readonly TriggerEventsProperty Properties;
```

Flags controlling this trigger's re-fire behavior, e.g. whether it should only ever interact once (`TriggerEventsProperty.OnlyInteractOnce`).

**Returns** \
[TriggerEventsProperty](../../Murder/Core/TriggerEventsProperty.html) \

#### Requirements

```csharp
[Tooltip("If none, this will always automatically start")]
public readonly ImmutableArray<RequirementsCollection> Requirements;
```

Alternative sets of blackboard/story requirements that can start this trigger. If empty, the trigger starts automatically (`CreateComponents` adds an `InteractOnStartComponent` in that case). If non-empty, each `RequirementsCollection` becomes an independent rule and the trigger fires as soon as any one of them matches.

**Returns** \
[ImmutableArray\<RequirementsCollection\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Triggers

```csharp
public readonly ImmutableArray<IInteractiveComponent> Triggers;
```

The interactions to run once this trigger fires. Wrapped into an `InteractionCollection` by `CreateComponents`.

**Returns** \
[ImmutableArray\<IInteractiveComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### World

```csharp
[Tooltip("Which world does this apply")]
[GameAssetId<WorldAsset>]
[Default("Only on world...")]
public readonly Guid? World;
```

Optional asset GUID of the `WorldAsset` this trigger should be scoped to. When set, authoring tools use this to restrict where the trigger is considered valid/relevant.

**Returns** \
[Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

### ⭐ Methods

#### CreateComponents()

```csharp
public IComponent[] CreateComponents()
```

Builds the runtime `IComponent`s that implement this trigger's behavior, ready to be added to an entity. When `Requirements` is empty, adds a single `InteractOnStartComponent` so the trigger fires immediately on start. Otherwise adds one `InteractOnRuleMatchCollectionComponent` containing one `InteractOnRuleMatchComponent` per entry in `Requirements` (using `AfterInteractRule.RemoveComponent` when `TriggerEventsProperty.OnlyInteractOnce` is set on `Properties`, otherwise `AfterInteractRule.Always`). Always appends an `InteractiveComponent<InteractionCollection>` wrapping the `Triggers` list so the actual interactions run when the rule matches.

**Returns** \
[IComponent[]](../../Bang/Components/IComponent.html) \

⚡

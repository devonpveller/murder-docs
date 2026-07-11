# IModifiableComponent

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public abstract IModifiableComponent : IComponent
```

A special type of component that can be modified.

Most Bang components are immutable `readonly struct` values: changing one means replacing it
wholesale via `Entity.ReplaceComponent`. `IModifiableComponent` is the escape hatch for the
opposite case — a component whose internal state can change *without* the entity replacing the
component instance itself (for example, a component that wraps a mutable collection, or one that
watches an external source of truth such as the save/blackboard system). Implementing this
interface tells Bang's `Entity` to treat the component specially: whenever the component is
attached, replaced, or removed, `Entity` calls `Subscribe`/`Unsubscribe` with an internal callback
so that when the component's own internal state changes, the entity is notified as if the
component had been replaced (`OnComponentModified` observers, tracked-context queries, and parent
notifications all fire correctly). Components implementing `IModifiableComponent` are also
special-cased during entity duplication/serialization (see `SerializationHelper.DeepCopy`,
used throughout `EntityBuilder`, `PrefabAsset`, and save loading) so that copies do not
accidentally share the same mutable, subscribed instance.

A concrete example is `RuleWatcherComponent` in `src\Murder\Components\Story\RuleWatcherComponent.cs`:
its `Subscribe` hooks into the save system's blackboard tracker (`BlackboardTracker.WatchAll`) so
that whenever a story/gameplay blackboard value changes, the registered `notification` callback
fires and the entity is treated as modified, without ever calling `ReplaceComponent`. Implement
this interface on a component when its "value" is really a view over something that mutates on its
own — never implement it just to make an otherwise-plain component mutable; a plain
`readonly struct` component replaced via `ReplaceComponent` is almost always the simpler, safer
choice.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Methods
#### Subscribe(Action)
```csharp
public abstract void Subscribe(Action notification)
```

Subscribe to receive notifications when the component gets modified.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)
```csharp
public abstract void Unsubscribe(Action notification)
```

Unsubscribe to stop receiving notifications when the component gets modified.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡
# AnimationEventBroadcasterComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationEventBroadcasterComponent : IComponent
```

Holds the set of entity IDs that should receive animation events fired by this entity's sprite.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Allows an entity's `AnimationEventMessage`s (fired when its sprite's Aseprite animation hits a named event frame) to be forwarded to a configurable set of listener entities, not just handled locally. Marked `[RuntimeOnly]` and `[PersistOnSave]` — despite being runtime-only, its subscription list is explicitly kept across saves (it does not use `[DoNotPersistOnSave]`) and it has a `[CustomName]` of `" AnimationEventBroadcaster"` for the editor's component picker.

**Use-case:** Rather than constructing or mutating this component directly, call the `EntityServices.SubscribeToAnimationEvents(listener, broadcaster)` extension method on the entity that should receive events, passing the entity whose sprite raises them; it takes care of adding the component if missing and adding `listener`'s ID to `BroadcastTo`. `AnimationEventBroadcastSystem` listens for `AnimationEventMessage` on any entity with this component and re-sends the message (with `BroadcastedEvent = true`) to every still-active entity in `BroadcastTo`, silently dropping any listener ID whose entity no longer exists or is inactive.

### ⭐ Constructors

```csharp
public AnimationEventBroadcasterComponent()
```

Creates a broadcaster with an empty listener set.

```csharp
public AnimationEventBroadcasterComponent(ImmutableHashSet<int> broadcastTo)
```

Creates a broadcaster pre-populated with the given set of listener entity IDs.

**Parameters** \
`broadcastTo` [ImmutableHashSet\<int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \

### ⭐ Properties

#### BroadcastTo

```csharp
public readonly ImmutableHashSet<int> BroadcastTo;
```

The set of entity IDs that will receive this entity's animation events. Populated via `EntityServices.SubscribeToAnimationEvents` and pruned automatically by `AnimationEventBroadcastSystem` as listener entities are removed or deactivated.

**Returns** \
[ImmutableHashSet\<int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \

⚡

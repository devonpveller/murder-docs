# AnimationEventBroadcasterComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationEventBroadcasterComponent : IComponent
```

Holds the set of entity IDs that should receive animation events fired by this entity's sprite.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Allows an entity's animation events to be forwarded to a configurable set of listener entities rather than only the entity itself.

**Use-case:** Attach to a sprite entity and subscribe listener entities via `Subscribe`; `AnimationEventBroadcastSystem` will then route events to every entity in `BroadcastTo`.

### ⭐ Constructors
```csharp
public AnimationEventBroadcasterComponent()
```

```csharp
public AnimationEventBroadcasterComponent(ImmutableHashSet<T> broadcastTo)
```

Creates a broadcaster pre-populated with the given set of listener entity IDs.

**Parameters** \
`broadcastTo` [ImmutableHashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \

### ⭐ Properties
#### BroadcastTo
```csharp
public readonly ImmutableHashSet<T> BroadcastTo;
```

The set of entity IDs that will receive this entity's animation events.

**Returns** \
[ImmutableHashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \


⚡
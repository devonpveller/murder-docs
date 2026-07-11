# Extensions

**Namespace:** Bang.Entities \
**Assembly:** Bang.dll

```csharp
public static class Extensions
```

Quality of life extensions for the default components declared in Bang.

Bang ships three "special" components/interfaces that every entity is expected to be able to carry: [PositionComponent](../../Murder/Components/PositionComponent.html) (an entity's location in the world), [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html) (its behavior state machine) and [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) (how it responds to player interaction). Because they are so common, each one gets its own reserved index in [BangComponentTypes](../../Bang/Entities/BangComponentTypes.html) (`Position`, `StateMachine`, `Interactive`) instead of going through the generic per-project component lookup, and this class layers a strongly-typed, allocation-free API on top of [Entity](../../Bang/Entities/Entity.html)'s generic, index-based `HasComponent`/`GetComponent`/`AddOrReplaceComponent`/`RemoveComponent` methods so callers never have to spell out `BangComponentTypes.Position` (etc.) themselves.

For each of the three components the same verb pattern repeats:
- `Has<Name>(Entity)` — whether the entity currently carries the component.
- `Get<Name>(Entity)` — fetch the component, asserting if it is missing (mirrors `Entity.GetComponent<T>()`).
- `TryGet<Name>(Entity)` — fetch the component, or `null` if missing, without asserting.
- `Set<Name>(Entity, ...)` — add or replace the component (void return).
- `With<Name>(Entity, ...)` — same as `Set`, but returns the `Entity` so calls can be chained while building up an entity.
- `Remove<Name>(Entity)` — remove the component, returning whether it was present.

`PositionComponent` is the one exception: since `Entity` already exposes a cached, boxing-free `GetPosition()` instance method (position is read far more often than any other component, so `Entity` keeps a dedicated field for it — see [Entity](../../Bang/Entities/Entity.html)), there is no `GetPosition(Entity)` extension here, and `SetPosition` additionally offers `Vector2`- and `(float x, float y)`-based overloads as a convenience on top of the `PositionComponent`-based one. A caller should reach for `entity.GetStateMachine()` / `entity.HasInteractive()` / `entity.SetPosition(x, y)` instead of manually computing `BangComponentTypes.*` indices or calling the generic `Entity` component methods directly.

### ⭐ Methods
#### HasInteractive(Entity)
```csharp
public bool HasInteractive(Entity e)
```

Checks whether this entity possesses a component of type [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) or not.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### HasPosition(Entity)
```csharp
public bool HasPosition(Entity e)
```

Checks whether this entity possesses a component of type [PositionComponent](../../Murder/Components/PositionComponent.html) or not.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### HasStateMachine(Entity)
```csharp
public bool HasStateMachine(Entity e)
```

Checks whether this entity possesses a component of type [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html) or not.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### RemoveInteractive(Entity)
```csharp
public bool RemoveInteractive(Entity e)
```

Removes the component of type [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### RemovePosition(Entity)
```csharp
public bool RemovePosition(Entity e)
```

Removes the component of type [PositionComponent](../../Murder/Components/PositionComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### RemoveStateMachine(Entity)
```csharp
public bool RemoveStateMachine(Entity e)
```

Removes the component of type [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### WithInteractive(Entity, IInteractiveComponent)
```csharp
public Entity WithInteractive(Entity e, IInteractiveComponent component)
```

Adds or replaces the component of type [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`component` [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
The same entity, `e`, so calls can be chained.

#### WithStateMachine(Entity, IStateMachineComponent)
```csharp
public Entity WithStateMachine(Entity e, IStateMachineComponent component)
```

Adds or replaces the component of type [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`component` [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
The same entity, `e`, so calls can be chained.

#### GetInteractive(Entity)
```csharp
public IInteractiveComponent GetInteractive(Entity e)
```

Gets a component of type [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) \
#### TryGetInteractive(Entity)
```csharp
public IInteractiveComponent TryGetInteractive(Entity e)
```

Gets a [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) if the entity has one, otherwise returns null.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) \
#### GetStateMachine(Entity)
```csharp
public IStateMachineComponent GetStateMachine(Entity e)
```

Gets a component of type [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html) \
#### TryGetStateMachine(Entity)
```csharp
public IStateMachineComponent TryGetStateMachine(Entity e)
```

Gets a [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html) if the entity has one, otherwise returns null.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html) \
#### TryGetPosition(Entity)
```csharp
public PositionComponent? TryGetPosition(Entity e)
```

Gets a [PositionComponent](../../Murder/Components/PositionComponent.html) if the entity has one, otherwise returns null. This is the non-asserting counterpart to `Entity.GetPosition()`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[PositionComponent?](../../Murder/Components/PositionComponent.html) \
#### SetInteractive(Entity, IInteractiveComponent)
```csharp
public void SetInteractive(Entity e, IInteractiveComponent component)
```

Adds or replaces the component of type [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`component` [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) \

#### SetPosition(Entity, PositionComponent)
```csharp
public void SetPosition(Entity e, PositionComponent component)
```

Adds or replaces the component of type [PositionComponent](../../Murder/Components/PositionComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`component` [PositionComponent](../../Murder/Components/PositionComponent.html) \

#### SetPosition(Entity, Vector2)
```csharp
public void SetPosition(Entity e, Vector2 position)
```

Adds or replaces the component of type [PositionComponent](../../Murder/Components/PositionComponent.html), constructing it from a `Vector2`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SetPosition(Entity, float, float)
```csharp
public void SetPosition(Entity e, float x, float y)
```

Adds or replaces the component of type [PositionComponent](../../Murder/Components/PositionComponent.html), constructing it from raw `x`/`y` coordinates.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetStateMachine(Entity, IStateMachineComponent)
```csharp
public void SetStateMachine(Entity e, IStateMachineComponent component)
```

Adds or replaces the component of type [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`component` [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html) \



⚡
# TetheredComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TetheredComponent : IComponent
```

Stores the set of active tether connections for an entity, each linking it to another entity at a desired distance.

**Intent:** Constrain an entity's position relative to one or more target entities using a simple distance-based tether: each fixed tick, the entity and each of its tether targets are nudged towards each other whenever they drift further apart than the configured separation distance.

**Use-case:** Attach to a follower or attached object entity; populate `TetherPoints` with [TetherPoint](../../Murder/Components/TetherPoint.html) entries describing each tether target and its desired distance. A `StaticComponent` on either side of a tether prevents that side from being moved by the constraint.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public TetheredComponent(ImmutableArray<T> tetherPoints)
```

Creates the component from a list of tether constraints. `TetherPointsDict` is built automatically from `tetherPoints`, keyed by each point's target entity ID.

**Parameters** \
`tetherPoints` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties

#### TetherPoints

```csharp
public readonly ImmutableArray<T> TetherPoints;
```

All tether constraints active on this entity, in the order they are resolved each tick.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### TetherPointsDict

```csharp
public readonly ImmutableDictionary<TKey, TValue> TetherPointsDict;
```

`TetherPoints` indexed by target entity ID, for fast per-target lookup. Built automatically from `TetherPoints` when the component is constructed; not exposed via the constructor directly.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

⚡

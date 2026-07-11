# TetheredComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TetheredComponent : IComponent
```

Stores the set of active tether connections for an entity, each linking it to another entity at a desired distance and angle.

**Intent:** Constrain an entity's position relative to one or more target entities using tether physics.

**Use-case:** Attach to a follower or attached object entity; populate `TetherPoints` with [TetherPoint](../../Murder/Components/TetherPoint.html) entries describing each tether target and its spring parameters.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public TetheredComponent(ImmutableArray<T> tetherPoints)
```

**Parameters** \
`tetherPoints` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### TetherPoints
```csharp
public readonly ImmutableArray<T> TetherPoints;
```

List of all tether connections active on this entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### TetherPointsDict
```csharp
public readonly ImmutableDictionary<TKey, TValue> TetherPointsDict;
```

Dictionary view of `TetherPoints` keyed by target entity ID for fast per-target lookup.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \


⚡
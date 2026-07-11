# Observer

**Namespace:** Bang.Contexts \
**Assembly:** Bang.dll

```csharp
public abstract class Observer
```

Base class for [Context](../../Bang/Contexts/Context.html). This exists to abstract the concept of
"something that watches a set of entities within a world" away from the concrete filtering
implementation — in practice, `Context` is the only implementation today, but the rest of Bang (systems,
the world) only depends on this abstraction, which shares implementation for any other class that
decides to tweak the observer behavior (which hasn't happened yet).

### ⭐ Properties
#### Entities
```csharp
public abstract virtual ImmutableArray<T> Entities { get; }
```

Entities that are currently watched in the world. This is the live result of whatever filtering strategy
the derived observer implements — for `Context`, these are the entities that currently satisfy the
owning system's declared filters and are active.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### World
```csharp
public readonly World World;
```

World that it observes. Every observer is created for, and permanently bound to, a single
[World](../../Bang/World.html) instance. This is how a system reaches back into the broader world (e.g.
to fetch other unique components, or spawn/destroy entities) from within its filtered
[Context](../../Bang/Contexts/Context.html).

**Returns** \
[World](../../Bang/World.html) \


⚡

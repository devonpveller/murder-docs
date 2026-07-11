# Context

**Namespace:** Bang.Contexts \
**Assembly:** Bang.dll

```csharp
public class Context : Observer, IDisposable
```

Context is the live, filtered view of entities that a system operates on. Each system declares its
interests via one or more [FilterAttribute](../../Bang/Systems/FilterAttribute.html) (e.g. "give me all
entities that have all of X and none of Y"); the [World](../../Bang/World.html) compiles those
declarations into a Context, which then incrementally tracks membership as entities are created,
destroyed, activated/deactivated, or have their components added, removed or modified — so the system's
`Entities`/`Entity` are always current without the system having to re-scan the whole world every frame.
Systems that declare the exact same filter share the same Context instance, so the same set of entities
is never tracked twice. Every `Update`/`FixedUpdate`/`Start`/`Exit`-style system callback receives its
Context as the argument to work with.

**Implements:** _[Observer](../../Bang/Contexts/Observer.html), [IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Properties
#### Entities
```csharp
public virtual ImmutableArray<T> Entities { get; }
```

Entities that are currently active in the context. This is a cached, immutable snapshot of every entity
that currently satisfies the context's filter and is enabled; the snapshot is rebuilt lazily the next
time it is requested after an entity has entered or left the context. This is what a system typically
iterates over on every update.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Entity
```csharp
public Entity Entity { get; }
```

Get the single entity present in the context. This assumes that the context targets a unique component,
i.e. that at most one entity is ever expected to match its filter. Only call this when `HasAnyEntity` is
known to be true; otherwise this asserts and will crash. Prefer `TryGetUniqueEntity()` whenever the
entity might legitimately be absent.
TODO: Add flag that checks for unique components within this context.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
#### HasAnyEntity
```csharp
public bool HasAnyEntity { get; }
```

Whether the context has any entity active. Useful to cheaply gate a system's per-frame work (e.g. skip
its update logic entirely, or bail out early during start/exit) when there is currently nothing to act
on, without paying the cost of materializing `Entities`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### World
```csharp
public readonly World World;
```

World that it observes. Every Context is created for, and permanently bound to, a single
[World](../../Bang/World.html) instance; this is how a system reaches back into the broader world (e.g.
to fetch other unique components, or spawn/destroy entities) from within its filtered context.

**Returns** \
[World](../../Bang/World.html) \
### ⭐ Methods
#### TryGetUniqueEntity()
```csharp
public Entity TryGetUniqueEntity()
```

Tries to get a unique entity, if none is available, returns null. This is meant for contexts that are
known to target a "singleton-like" component, where at most one entity is expected to match the filter
at any given time. Unlike `Entity`, this does not assert when there is no match, so it is safe to call
even before such an entity has been created in the world.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
\

#### Dispose()
```csharp
public virtual void Dispose()
```

Disposes of the context. Called by [World](../../Bang/World.html) when the world is torn down. Clears
every subscription this context holds on entity change notifications and empties the tracked entity
collection, so neither the context nor the systems it feeds keep entities alive past the world's
lifetime.



⚡

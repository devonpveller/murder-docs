# UniqueAttribute

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public class UniqueAttribute : Attribute
```

Marks a component as unique within our world.
            We should not expect two entities with the same component if it is declared as unique.

`[Unique]` documents (and, in diagnostics builds, helps enforce) an intentional design
constraint: at most one entity in a given [World](../../Bang/World.html) should carry this
component at a time. This is the idiomatic way to model "singleton" game state as an ECS
component instead of a global/static field — for example a world-wide watcher such as
`RuleWatcherComponent` (`src\Murder\Components\Story\RuleWatcherComponent.cs`), which tracks
blackboard rule changes for the whole save file and would make no sense duplicated across
entities. Systems that query for a `[Unique]` component can safely assume they will get zero or
one matches back instead of having to handle an arbitrary collection, which both simplifies system
code and documents intent for anyone (including an autonomous agent) adding a new entity to the
world: if you are about to attach a `[Unique]` component to a second entity, that is almost always
a bug rather than a valid use case. Apply this attribute to the component's struct declaration,
alongside other component attributes such as
[RequiresAttribute](../../Bang/Components/RequiresAttribute.html) or
[KeepOnReplaceAttribute](../../Bang/Components/KeepOnReplaceAttribute.html).

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public UniqueAttribute()
```

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
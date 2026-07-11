# WatchAttribute

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public class WatchAttribute : Attribute
```

Declares which component types an [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html) wants to be notified about
            when they are added, removed, or modified on an entity. This is required for every system
            that implements [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html) - without it, [World](../../Bang/World.html) has nothing
            to subscribe the system's watcher to, and (in diagnostics mode) attaching
            this attribute to a system that is not an [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html) is asserted against
            and silently dropped. Pair it with a [FilterAttribute](../../Bang/Systems/FilterAttribute.html) describing the overall
            entity shape the system operates on; [WatchAttribute](../../Bang/Systems/WatchAttribute.html) then narrows that down to
            the specific component(s) whose changes actually trigger `IReactiveSystem.OnAdded`,
            `IReactiveSystem.OnModified` or `IReactiveSystem.OnRemoved`.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public WatchAttribute(Type[] types)
```

Creates a new [WatchAttribute](../../Bang/Systems/WatchAttribute.html) with a set of target types.

**Parameters** \
`types` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
#### Types
```csharp
public Type[] Types { get; }
```

The component types that, when added, removed or modified on an entity, will notify
            the owning [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html).

**Returns** \
[Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \


⚡

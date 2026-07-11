# FilterAttribute

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public class FilterAttribute : Attribute
```

Declares which entities a system cares about: "give me every entity that has all of X and
            none of Y", for example. Every concrete [ISystem](../../Bang/Systems/ISystem.html) that wants entities delivered
            to it (via a [Context](../../Bang/Contexts/Context.html)) should carry at least one
            [FilterAttribute](../../Bang/Systems/FilterAttribute.html) - [World](../../Bang/World.html) reads it via reflection when the world
            is built and compiles it
            into the incrementally-tracked entity set exposed as `Context.Entities`. The attribute
            is repeatable (`AllowMultiple = true`): stack several [FilterAttribute](../../Bang/Systems/FilterAttribute.html)s on
            the same system to combine filters, e.g. one [ContextAccessorFilter.AllOf](../../Bang/Contexts/ContextAccessorFilter.html) filter
            for the required components plus a second [ContextAccessorFilter.NoneOf](../../Bang/Contexts/ContextAccessorFilter.html) filter
            for components that should exclude the entity. This applies uniformly to every kind of
            system - [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html),
            [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [IMessagerSystem](../../Bang/Systems/IMessagerSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html) -
            since it only shapes *which entities* the context sees; it is orthogonal to
            [WatchAttribute](../../Bang/Systems/WatchAttribute.html) and [MessagerAttribute](../../Bang/Systems/MessagerAttribute.html), which instead declare
            *which changes or messages* on top of that entity set should trigger a notification.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public FilterAttribute(ContextAccessorFilter filter, ContextAccessorKind kind, Type[] types)
```

Creates a system filter with custom accessors.

**Parameters** \
`filter` [ContextAccessorFilter](../../Bang/Contexts/ContextAccessorFilter.html) \
`kind` [ContextAccessorKind](../../Bang/Contexts/ContextAccessorKind.html) \
`types` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

```csharp
public FilterAttribute(ContextAccessorFilter filter, Type[] types)
```

Create a system filter with default accessor of [Kind](../../Bang/Systems/FilterAttribute.html) for `types`.

**Parameters** \
`filter` [ContextAccessorFilter](../../Bang/Contexts/ContextAccessorFilter.html) \
`types` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

```csharp
public FilterAttribute(ContextAccessorKind kind, Type[] types)
```

Create a system filter with default accessor of [Filter](../../Bang/Systems/FilterAttribute.html) for `types`.

**Parameters** \
`kind` [ContextAccessorKind](../../Bang/Contexts/ContextAccessorKind.html) \
`types` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

```csharp
public FilterAttribute(Type[] types)
```

Create a system filter with default accessors for `types`.

**Parameters** \
`types` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

### ⭐ Properties
#### Filter
```csharp
public ContextAccessorFilter Filter { get; public set; }
```

This is how the system will filter the entities. See [ContextAccessorFilter](../../Bang/Contexts/ContextAccessorFilter.html).

**Returns** \
[ContextAccessorFilter](../../Bang/Contexts/ContextAccessorFilter.html) \
#### Kind
```csharp
public ContextAccessorKind Kind { get; public set; }
```

This is the kind of accessor that will be made on this component.
            This can be leveraged once we parallelize update frames (which we don't yet), so don't bother with this just yet.

**Returns** \
[ContextAccessorKind](../../Bang/Contexts/ContextAccessorKind.html) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
#### Types
```csharp
public Type[] Types { get; public set; }
```

System will target all the entities that has all this set of components.

**Returns** \
[Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \


⚡

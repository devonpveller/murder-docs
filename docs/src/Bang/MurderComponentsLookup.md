# MurderComponentsLookup

**Namespace:** Bang \
**Assembly:** Murder.dll

```csharp
public class MurderComponentsLookup : ComponentsLookup
```

Auto-generated implementation of [ComponentsLookup](../Bang/ComponentsLookup.html) for this project.

This class is emitted at compile time by `Bang.Generator` (see `Templates.LookupImplementation` in
`Bang.Generator/Templating`), which scans the Murder project for every declared component and message
— including components synthesized from `IStateMachineComponent`/`IInteractiveComponent` state machines
and interactions — and assigns each one a stable integer id. Those ids populate `ComponentsIndex` and
`MessagesIndex`, and any id belonging to a component that implements
[IParentRelativeComponent](../Bang/Components/IParentRelativeComponent.html) is also added to `RelativeComponents`. `MurderNextLookupId` records how
many ids this class allocated, offset from [ComponentsLookup.NextLookupId](../Bang/ComponentsLookup.html#nextlookupid), so that a project that in
turn depends on Murder (and generates its own lookup on top of this one) keeps allocating non-overlapping
ids.

You should never need to construct or reference this class directly — [World](../Bang/World.html) discovers it automatically
via [World.FindLookupImplementation](../Bang/World.html#findlookupimplementation) (reflection over loaded assemblies) the first time a world is created, and
uses it internally every time a component or message type needs to be resolved to its id, for example
inside [ComponentsLookup.Id(Type)](../Bang/ComponentsLookup.html#idtype). If you are adding a new component/message type to the project and this page
looks out of date, that's expected: just rebuild — the generator re-runs automatically and this file is
regenerated from scratch, so it should never be hand-edited. This page exists so the exact id mapping for
the current build is inspectable, e.g. when debugging serialization or save-data compatibility across
versions.

**Implements:** _[ComponentsLookup](../Bang/ComponentsLookup.html)_

### ⭐ Constructors
```csharp
public MurderComponentsLookup()
```

Default constructor. This is only relevant for the internals of Bang, so you can ignore it.

### ⭐ Properties
#### ComponentsIndex
```csharp
protected ImmutableDictionary<TKey, TValue> ComponentsIndex { get; protected set; }
```

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### MessagesIndex
```csharp
protected ImmutableDictionary<TKey, TValue> MessagesIndex { get; protected set; }
```

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### MurderNextLookupId
```csharp
public static int MurderNextLookupId { get; }
```

First lookup id a [ComponentsLookup](../Bang/ComponentsLookup.html) implementation that inherits from this class must use.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### RelativeComponents
```csharp
public ImmutableHashSet<T> RelativeComponents { get; protected set; }
```

**Returns** \
[ImmutableHashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \
### ⭐ Methods
#### IsRelative(int)
```csharp
public bool IsRelative(int id)
```

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Id(Type)
```csharp
public int Id(Type t)
```

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
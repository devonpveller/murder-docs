# ComponentsLookup

**Namespace:** Bang \
**Assembly:** Bang.dll

```csharp
public abstract class ComponentsLookup
```

Implemented by generators in order to provide a mapping of all the types to their respective id.

Every [Entity](../Bang/Entities/Entity.html) stores its components in a flat array indexed by a small integer rather than by `Type`,
since that is far cheaper to look up and store than a type-keyed collection. A `ComponentsLookup` is
what maps each [IComponent](../Bang/Components/IComponent.html) and [IMessage](../Bang/Components/IMessage.html) type to that integer id.

This base class only knows about the handful of ids that Bang itself requires (see
[BangComponentTypes](../Bang/Entities/BangComponentTypes.html)). Concrete implementations — such as the Bang.Generator-produced
`ComponentsLookup` for a game project — extend [ComponentsIndex](../Bang/ComponentsLookup.html#componentsindex),
[MessagesIndex](../Bang/ComponentsLookup.html#messagesindex) and [RelativeComponents](../Bang/ComponentsLookup.html#relativecomponents) with every component/message declared in
that project, starting at [NextLookupId](../Bang/ComponentsLookup.html#nextlookupid) (or the derived project's own equivalent constant) so
ids never collide across inheriting projects.

Types that are looked up but were not registered by a generator (e.g. dynamically declared in a script,
or simply forgotten by a generator run) still resolve correctly through [Id(Type)](../Bang/ComponentsLookup.html#idtype), but fall back to a
slower dictionary lookup tracked internally by this class.

### ⭐ Constructors
```csharp
protected ComponentsLookup()
```

### ⭐ Properties
#### ComponentsIndex
```csharp
protected ImmutableDictionary<TKey, TValue> ComponentsIndex { get; protected set; }
```

Maps all the components to their unique id.

Seeded with the ids Bang itself owns ([IStateMachineComponent](../Bang/StateMachines/IStateMachineComponent.html), [IInteractiveComponent](../Bang/Interactions/IInteractiveComponent.html) and
`PositionComponent`). Generated subclasses override this with the full set of components declared in
their project.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### MessagesIndex
```csharp
protected ImmutableDictionary<TKey, TValue> MessagesIndex { get; protected set; }
```

Maps all the messages to their unique id.

Empty by default — Bang itself does not declare any built-in messages. Generated subclasses override
this with the full set of [IMessage](../Bang/Components/IMessage.html) types declared in their project.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### NextLookupId
```csharp
public static const int NextLookupId;
```

Tracks the last id this particular implementation is tracking plus one.

This base class reserves ids for [IStateMachineComponent](../Bang/StateMachines/IStateMachineComponent.html), [IInteractiveComponent](../Bang/Interactions/IInteractiveComponent.html) and
`PositionComponent` (see [BangComponentTypes](../Bang/Entities/BangComponentTypes.html)), hence the value of 3. A generated subclass that adds
its own components should expose an equivalent constant that starts counting from this value, so that
any further derived lookup (e.g. a game project extending a shared library project) can keep allocating
non-overlapping ids.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### RelativeComponents
```csharp
public ImmutableHashSet<T> RelativeComponents { get; protected set; }
```

List of all the unique id of the components that inherit from [IParentRelativeComponent](../Bang/Components/IParentRelativeComponent.html).

A parent-relative component (such as the built-in `PositionComponent`) stores a value that is relative
to its entity's parent, if any. This set lets [IsRelative(int)](../Bang/ComponentsLookup.html#isrelativeint) answer that question purely from a
component id, without needing to inspect the component type itself.

**Returns** \
[ImmutableHashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \
### ⭐ Methods
#### IsRelative(int)
```csharp
public bool IsRelative(int id)
```

Returns whether the component with the given <paramref name="id" /> is relative to its parent, i.e.
whether it implements [IParentRelativeComponent](../Bang/Components/IParentRelativeComponent.html).

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
A component id, as returned by [Id(Type)](../Bang/ComponentsLookup.html#idtype). \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Id(Type)
```csharp
public int Id(Type t)
```

Get the id for <paramref name="t" />, which must be an [IComponent](../Bang/Components/IComponent.html) or [IMessage](../Bang/Components/IMessage.html) type.

Looks up <paramref name="t" /> first in [MessagesIndex](../Bang/ComponentsLookup.html#messagesindex) (if it is a message), then in
[ComponentsIndex](../Bang/ComponentsLookup.html#componentsindex). If neither generated table has an entry — most commonly because
<paramref name="t" /> was declared without a generator run for its project — the id is computed and
cached lazily instead, at a lower performance cost for that particular type.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
An [IComponent](../Bang/Components/IComponent.html) or [IMessage](../Bang/Components/IMessage.html) type. \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The unique id associated with `t`.



⚡
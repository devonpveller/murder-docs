# TriggerEventOn

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct TriggerEventOn
```

Describes a named trigger event, including optional component requirements, the set of interaction targets, an optional world reference, and a flag to fire only once.

**Intent:** Data container that bundles all parameters needed to fire a specific trigger event from within an interaction or action.

**Use-case:** Added to interaction assets or components to specify which named event fires, when its requirements are met, and which entities or worlds are targeted.

### ⭐ Constructors
```csharp
public TriggerEventOn()
```

Creates an empty `TriggerEventOn` with no name, requirements, or targets.

```csharp
public TriggerEventOn(string name)
```

Creates a `TriggerEventOn` with the specified event name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Name
```csharp
public readonly string Name;
```

The name of the trigger event to fire.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### OnlyOnce
```csharp
public readonly bool OnlyOnce;
```

When `true`, this trigger fires at most once and is then disabled.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Requirements
```csharp
public readonly ImmutableArray<T> Requirements;
```

Component-type requirements that must all be satisfied on the triggering entity before this event fires.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Triggers
```csharp
public readonly ImmutableArray<T> Triggers;
```

The set of interaction instances that this event will execute when triggered.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### World
```csharp
public readonly T? World;
```

An optional reference to a world asset or entity that should receive this trigger event.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
### ⭐ Methods
#### CreateComponents()
```csharp
public IComponent[] CreateComponents()
```

Instantiates the components defined by this trigger's interaction list so they can be added to an entity at runtime.

**Returns** \
[IComponent[]](../../Bang/Components/IComponent.html) \



⚡
# Situation

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct Situation
```

A named collection of `Dialog` nodes and their outgoing `DialogEdge` transitions, representing one addressable dialogue state for a character.

**Intent:** Groups all the dialogue nodes that belong to a single logical conversation topic or game state into a named, indexable unit that the runtime can activate by name.

**Use-case:** A character asset holds a dictionary of `Situation`s; `CharacterRuntime.StartAtSituation` selects the active one by name, after which the runtime traverses its `Dialogs` and `Edges` to drive the conversation.

### ⭐ Constructors

```csharp
public Situation()
```

Creates an empty situation with default values.

```csharp
public Situation(int id, string name, ImmutableArray<T> dialogs, ImmutableDictionary<TKey, TValue> edges)
```

Full constructor that populates all fields of the situation.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`dialogs` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`edges` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

```csharp
public Situation(int id, string name)
```

Creates a situation with the given id and name but no dialogs or edges.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Dialogs

```csharp
public readonly ImmutableArray<T> Dialogs;
```

Ordered list of all `Dialog` nodes that belong to this situation.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Edges

```csharp
public readonly ImmutableDictionary<TKey, TValue> Edges;
```

Map from a source dialog id to the `DialogEdge` that describes how to transition to the next dialog.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### Id

```csharp
public readonly int Id;
```

Unique integer identifier for this situation within the character's situation list.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Name

```csharp
public readonly string Name;
```

Human-readable name used by `CharacterRuntime.StartAtSituation` to look up and activate this situation.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### WithDialogAt(int, Dialog)

```csharp
public Situation WithDialogAt(int index, Dialog dialog)
```

Returns a copy of this situation with the `Dialog` at `index` replaced.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`dialog` [Dialog](../../../Murder/Core/Dialogs/Dialog.html) \

**Returns** \
[Situation](../../../Murder/Core/Dialogs/Situation.html) \

#### WithName(string)

```csharp
public Situation WithName(string name)
```

Returns a copy of this situation with the `Name` replaced.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Situation](../../../Murder/Core/Dialogs/Situation.html) \

⚡

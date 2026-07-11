# Dialog

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct Dialog
```

A single dialogue node: an ordered list of `Line`s protected by `CriterionNode` requirements, with optional `DialogAction`s to execute and an outgoing edge target.

**Intent:** Represents one "page" of dialogue within a `Situation` — the content to display, the conditions that must be met for it to be eligible, how many times it can play, and where to go next.

**Use-case:** Author nodes in the dialogue editor; at runtime `CharacterRuntime` evaluates `Requirements`, advances through `Lines`, fires `Actions`, and follows `GoTo` (or the situation's `DialogEdge`) when the node is complete.

### ⭐ Constructors
```csharp
public Dialog()
```

Creates a default dialog node with no lines, requirements, or actions and `PlayUntil` set to `-1` (play forever).

```csharp
public Dialog(int id, int playUntil, ImmutableArray<T> requirements, ImmutableArray<T> lines, T? actions, T? goto, bool isChoice)
```

Full constructor that initialises all fields of the dialog node.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`playUntil` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`requirements` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`lines` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`actions` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`goto` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`isChoice` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### Actions
```csharp
public readonly T? Actions;
```

Optional list of `DialogAction`s executed when this node is visited (e.g. setting blackboard variables).

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### GoTo
```csharp
public readonly T? GoTo;
```

Go to another dialog with a specified id.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Id
```csharp
public readonly int Id;
```

Unique integer identifier for this dialog node within its parent `Situation`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### IsChoice
```csharp
public readonly bool IsChoice;
```

When `true`, this node presents player-selectable choices rather than playing lines automatically.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Lines
```csharp
public readonly ImmutableArray<T> Lines;
```

The ordered list of `Line`s to display when this dialog node is active.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### PlayUntil
```csharp
public readonly int PlayUntil;
```

Stop playing this dialog until this number.
            If -1, this will play forever.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Requirements
```csharp
public readonly ImmutableArray<T> Requirements;
```

The set of `CriterionNode` conditions that must be satisfied for this dialog node to be eligible during selection.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### WithActions(T?)
```csharp
public Dialog WithActions(T? actions)
```

Returns a copy of this dialog with the `Actions` list replaced.

**Parameters** \
`actions` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[Dialog](../../../Murder/Core/Dialogs/Dialog.html) \

#### WithLineAt(int, Line)
```csharp
public Dialog WithLineAt(int index, Line line)
```

Returns a copy of this dialog with the `Line` at position `index` replaced.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`line` [Line](../../../Murder/Core/Dialogs/Line.html) \

**Returns** \
[Dialog](../../../Murder/Core/Dialogs/Dialog.html) \

#### DebuggerDisplay()
```csharp
public string DebuggerDisplay()
```

Returns a compact debug string showing the node id, requirement count, line count, and action count.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡
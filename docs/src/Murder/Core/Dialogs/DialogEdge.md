# DialogEdge

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct DialogEdge
```

A directed edge in the dialogue graph that maps a source `Dialog` node to one or more candidate successor nodes, together with the selection strategy.

**Intent:** Encodes the outgoing transitions from a dialog node, listing the eligible successors and how to pick among them (sequentially, randomly, by score, or as a choice).

**Use-case:** Stored in `Situation.Edges` keyed by source dialog id; `CharacterRuntime` reads the edge after completing a node's lines to determine which dialog to visit next.

### ⭐ Constructors

```csharp
public DialogEdge(MatchKind kind, ImmutableArray<T> dialogs)
```

Creates an edge with the given selection strategy and list of candidate dialog ids.

**Parameters** \
`kind` [MatchKind](../../../Murder/Core/Dialogs/MatchKind.html) \
`dialogs` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties

#### Dialogs

```csharp
public readonly ImmutableArray<T> Dialogs;
```

Ordered list of dialog IDs that are candidates for the next step; which one is chosen depends on `Kind`.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Kind

```csharp
public readonly MatchKind Kind;
```

The strategy used to select the next dialog from `Dialogs` (e.g. `Next`, `Random`, `HighestScore`, `Choice`).

**Returns** \
[MatchKind](../../../Murder/Core/Dialogs/MatchKind.html) \

### ⭐ Methods

#### DebuggerDisplay()

```csharp
public string DebuggerDisplay()
```

Returns a compact debug string showing the edge's `Kind` and the set of target dialog ids.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

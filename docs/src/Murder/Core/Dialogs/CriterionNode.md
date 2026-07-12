# CriterionNode

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct CriterionNode
```

Pairs a `Criterion` with a `CriterionNodeKind` combinator, forming one node in a logical expression tree used to gate dialogue.

**Intent:** Wraps a single condition together with its boolean role (`And` / `Or`) so that a flat list of nodes can be evaluated as a compound logical expression.

**Use-case:** Add `CriterionNode` values to `Dialog.Requirements`; the runtime traverses the list and short-circuits evaluation according to each node's `Kind` to decide whether a dialog node is eligible to play.

### ⭐ Constructors

```csharp
public CriterionNode()
```

Creates an empty node with default `Criterion` and `CriterionNodeKind.And`.

```csharp
public CriterionNode(Criterion criterion, CriterionNodeKind kind)
```

Creates a node with an explicit criterion and combinator kind.

**Parameters** \
`criterion` [Criterion](../../../Murder/Core/Dialogs/Criterion.html) \
`kind` [CriterionNodeKind](../../../Murder/Core/Dialogs/CriterionNodeKind.html) \

```csharp
public CriterionNode(Criterion criterion)
```

Creates a node with the given criterion and the default combinator `CriterionNodeKind.And`.

**Parameters** \
`criterion` [Criterion](../../../Murder/Core/Dialogs/Criterion.html) \

### ⭐ Properties

#### Criterion

```csharp
public readonly Criterion Criterion;
```

The individual condition this node represents.

**Returns** \
[Criterion](../../../Murder/Core/Dialogs/Criterion.html) \

#### Kind

```csharp
public readonly CriterionNodeKind Kind;
```

Determines how this node is combined with adjacent nodes in the requirements list (`And` or `Or`).

**Returns** \
[CriterionNodeKind](../../../Murder/Core/Dialogs/CriterionNodeKind.html) \

### ⭐ Methods

#### WithCriterion(Criterion)

```csharp
public CriterionNode WithCriterion(Criterion criterion)
```

Returns a copy of this node with the `Criterion` replaced.

**Parameters** \
`criterion` [Criterion](../../../Murder/Core/Dialogs/Criterion.html) \

**Returns** \
[CriterionNode](../../../Murder/Core/Dialogs/CriterionNode.html) \

#### WithKind(CriterionNodeKind)

```csharp
public CriterionNode WithKind(CriterionNodeKind kind)
```

Returns a copy of this node with the combinator `Kind` replaced.

**Parameters** \
`kind` [CriterionNodeKind](../../../Murder/Core/Dialogs/CriterionNodeKind.html) \

**Returns** \
[CriterionNode](../../../Murder/Core/Dialogs/CriterionNode.html) \

#### DebuggerDisplay()

```csharp
public string DebuggerDisplay()
```

Returns a compact debug string showing the fact name, comparison operator, and value, used by the type's `[DebuggerDisplay]` attribute.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

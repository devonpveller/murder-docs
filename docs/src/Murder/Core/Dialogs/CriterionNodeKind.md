# CriterionNodeKind

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed enum CriterionNodeKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Controls how a `CriterionNode` is logically combined with the preceding nodes in a requirements list.

**Intent:** Provides the `And` / `Or` connective for building compound dialogue conditions from a flat list of `CriterionNode` entries.

**Use-case:** Set `CriterionNode.Kind` to `And` when all conditions must hold simultaneously, or `Or` when any one of them is sufficient to unlock the dialog.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### And

```csharp
public static const CriterionNodeKind And;
```

This node's criterion is combined with the previous result using logical AND; all `And` nodes in the group must pass.

**Returns** \
[CriterionNodeKind](../../../Murder/Core/Dialogs/CriterionNodeKind.html) \

#### Or

```csharp
public static const CriterionNodeKind Or;
```

This node's criterion is combined with the previous result using logical OR; the overall condition passes if any `Or`-connected node passes.

**Returns** \
[CriterionNodeKind](../../../Murder/Core/Dialogs/CriterionNodeKind.html) \

⚡

# BlackboardActionKind

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed enum BlackboardActionKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Defines the operation to perform on a blackboard fact when a `DialogAction` is executed.

**Intent:** Enumerates every mutation that can be applied to a blackboard variable — assignment, arithmetic, boolean toggling, or component modification.

**Use-case:** Assign a value to `DialogAction.Kind` to control how a fact is mutated when a dialogue node is visited.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Add
```csharp
public static const BlackboardActionKind Add;
```

Increments an integer or float fact by the specified value.

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
#### Component
```csharp
public static const BlackboardActionKind Component;
```

Adds or replaces a component on the target entity instead of modifying a named fact.

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
#### Minus
```csharp
public static const BlackboardActionKind Minus;
```

Decrements an integer or float fact by the specified value.

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
#### Set
```csharp
public static const BlackboardActionKind Set;
```

Assigns the specified value directly to the fact, replacing any existing value.

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
#### SetMax
```csharp
public static const BlackboardActionKind SetMax;
```

Sets the fact to the higher of its current value and the specified value, clamping downward changes.

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
#### SetMin
```csharp
public static const BlackboardActionKind SetMin;
```

Sets the fact to the lower of its current value and the specified value, clamping upward changes.

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
#### Toggle
```csharp
public static const BlackboardActionKind Toggle;
```

Flips a boolean fact from `true` to `false` or vice versa.

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \


⚡
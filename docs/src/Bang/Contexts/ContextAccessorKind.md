# ContextAccessorKind

**Namespace:** Bang.Contexts \
**Assembly:** Bang.dll

```csharp
public sealed enum ContextAccessorKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Context accessor kind for a system. This will specify the kind of operation that each system will
perform, so the world can parallelize efficiently each system execution. It is declared per filtered
component type via [FilterAttribute](../../Bang/Systems/FilterAttribute.html)'s `Kind` property; today
[Context](../../Bang/Contexts/Context.html) tracks this information internally (per component index),
but it is not yet consumed to actually schedule systems in parallel — the plumbing exists so that future
work can do so safely.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Read
```csharp
public static const ContextAccessorKind Read;
```

This will specify that the system implementation will only perform read operations. Two systems that
both only Read the same component could safely run concurrently once parallel system execution is
implemented.

**Returns** \
[ContextAccessorKind](../../Bang/Contexts/ContextAccessorKind.html) \
#### Write
```csharp
public static const ContextAccessorKind Write;
```

This will specify that the system implementation will only perform write operations. A system that
Writes a component conflicts with any other system that Reads or Writes that same component, and
therefore cannot be scheduled to run concurrently with it.

**Returns** \
[ContextAccessorKind](../../Bang/Contexts/ContextAccessorKind.html) \


⚡

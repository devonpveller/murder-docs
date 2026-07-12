# InteractOn

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed enum InteractOn : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies the condition under which an `InteractOnRuleMatchComponent` rule is evaluated and can trigger an interaction.

**Intent:** Control whether a rule fires both when its underlying blackboard value is first set and when it changes, or only on subsequent changes.

**Use-case:** Set on `InteractOnRuleMatchComponent.InteractOn` to tune when exactly the associated interaction fires relative to blackboard state changes.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### AddedOrModified

```csharp
public static const InteractOn AddedOrModified;
```

The rule fires both when the tracked blackboard value is first added (set) and whenever it is subsequently modified.

**Returns** \
[InteractOn](../../Murder/Components/InteractOn.html) \

#### Modified

```csharp
public static const InteractOn Modified;
```

The rule fires only when the tracked blackboard value changes after it has already been set at least once.

**Returns** \
[InteractOn](../../Murder/Components/InteractOn.html) \

⚡

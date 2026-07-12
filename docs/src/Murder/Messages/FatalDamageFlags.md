# FatalDamageFlags

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
[Flags]
public sealed enum FatalDamageFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Bitwise modifiers carried by [FatalDamageMessage](../../Murder/Messages/FatalDamageMessage.html) that change how death should be handled, beyond just "this entity died".

**Intent:** Let the sender of a fatal-damage notification opt out of default on-death behavior without needing a separate message type or a bespoke component. The engine itself does not branch on these flags — they exist for game-specific death-handling systems to read.

**Use-case:** Pass `FatalDamageFlags.IgnoreDrop` into `new FatalDamageMessage(flags)` (or the generated `entity.SendFatalDamageMessage(flags)` extension) when an entity should die without triggering its usual loot/item drop logic — for example when a container or enemy is destroyed by scripted/cutscene logic rather than combat. Being `[Flags]`, values can be OR'd together as more modifiers are added.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### None

```csharp
public static const FatalDamageFlags None;
```

No modifiers; the fatal damage should be handled with default death behavior. This is the default value used by [FatalDamageMessage](../../Murder/Messages/FatalDamageMessage.html)'s parameterless and `(fromId, damagedEntityId)` constructors.

**Returns** \
[FatalDamageFlags](../../Murder/Messages/FatalDamageFlags.html) \

#### IgnoreDrop

```csharp
public static const FatalDamageFlags IgnoreDrop;
```

Requests that whatever item/loot drop behavior normally runs on this entity's death be skipped.

**Returns** \
[FatalDamageFlags](../../Murder/Messages/FatalDamageFlags.html) \

⚡

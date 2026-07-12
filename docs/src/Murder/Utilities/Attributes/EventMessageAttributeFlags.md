# EventMessageAttributeFlags

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public sealed enum EventMessageAttributeFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Controls how the editor discovers and propagates the event message names declared by an [EventMessagesAttribute](../../../Murder/Utilities/Attributes/EventMessagesAttribute.html).

**Intent:** Fine-tunes whether the editor validates messages via a component method or propagates them to a parent entity.

**Use-case:** Pass one or more of these flags (OR'd together) into `EventMessagesAttribute`'s constructor to change how `StageHelpers.CheckForAttributeEventsOnType` surfaces the declared events while authoring animations/interactions in the editor.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### CheckDisplayOnlyIf

```csharp
public static const EventMessageAttributeFlags CheckDisplayOnlyIf;
```

This will check for a method in the component of name: "VerifyEventMessages" before
displaying them in the editor.

**Returns** \
[EventMessageAttributeFlags](../../../Murder/Utilities/Attributes/EventMessageAttributeFlags.html) \

#### None

```csharp
public static const EventMessageAttributeFlags None;
```

No special handling: the declared events are always shown for the component, and are not propagated to a parent entity when the component belongs to a child.

**Returns** \
[EventMessageAttributeFlags](../../../Murder/Utilities/Attributes/EventMessageAttributeFlags.html) \

#### PropagateToParent

```csharp
public static const EventMessageAttributeFlags PropagateToParent;
```

When the component carrying `EventMessagesAttribute` lives on a child entity, its declared events are also surfaced on the parent entity's event list.

**Returns** \
[EventMessageAttributeFlags](../../../Murder/Utilities/Attributes/EventMessageAttributeFlags.html) \

⚡

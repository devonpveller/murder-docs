# EventMessagesAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class EventMessagesAttribute : Attribute
```

Notifies the editor that a set of events is available on this entity.

**Intent:** Declares which Bang event-message names a component or system listens to.

**Use-case:** Decorate a system class with this attribute so the editor can list and validate available event messages for that system's target entities.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public EventMessagesAttribute(EventMessageAttributeFlags flags, String[] events)
```

Declares event messages with the given flags and event name array.

**Parameters** \
`flags` [EventMessageAttributeFlags](../../../Murder/Utilities/Attributes/EventMessageAttributeFlags.html) \
`events` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

```csharp
public EventMessagesAttribute(String[] events)
```

Declares event messages without special flags.

**Parameters** \
`events` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Events
```csharp
public readonly String[] Events;
```

Array of event message names declared by this attribute.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Flags
```csharp
public readonly EventMessageAttributeFlags Flags;
```

Flags controlling how the editor discovers and propagates these events.

**Returns** \
[EventMessageAttributeFlags](../../../Murder/Utilities/Attributes/EventMessageAttributeFlags.html) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
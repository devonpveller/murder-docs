# EventMessagesAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class EventMessagesAttribute : Attribute
```

Declares, on an [IComponent](../../../Bang/Components/IComponent.html) type, which Bang event-message names entities carrying it can raise.

**Intent:** Lets the editor's animation/interaction tooling offer a validated list of event names instead of requiring designers to type a message name by hand.

**Use-case:** Apply to an `IComponent` type (typically an interactive component) to declare the events it can raise, e.g. `[EventMessages("OnDamage", "OnDeath")]`. The editor's `StageHelpers.CheckForAttributeEventsOnType` reads this attribute when populating the event pickers used for binding animation-frame events or interaction events in the inspector. Combine with [EventMessageAttributeFlags](../../../Murder/Utilities/Attributes/EventMessageAttributeFlags.html) to also gate display behind a `VerifyEventMessages` method or to propagate events declared on a child component up to its parent.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public EventMessagesAttribute(String[] events)
```

Declares `events` with no special flags.

**Parameters** \
`events` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

```csharp
public EventMessagesAttribute(EventMessageAttributeFlags flags, String[] events)
```

Declares `events` with the given discovery/propagation `flags`.

**Parameters** \
`flags` [EventMessageAttributeFlags](../../../Murder/Utilities/Attributes/EventMessageAttributeFlags.html) \
`events` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

```csharp
public EventMessagesAttribute(EventMessageAttributeFlags flags, String[] events, String[] spriteFields)
```

Declares `events` with `flags`, additionally instructing the editor to also look for sprite-driven events on the component's `spriteFields` (fields holding a sprite/animation reference), merging events defined on the referenced sprite asset into the same list.

**Parameters** \
`flags` [EventMessageAttributeFlags](../../../Murder/Utilities/Attributes/EventMessageAttributeFlags.html) \
`events` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`spriteFields` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### CheckForSpriteFields

```csharp
public readonly String[]? CheckForSpriteFields;
```

Names of fields on the component whose sprite events should also be checked, or `null` if none. Set via the three-argument constructor.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Events

```csharp
public readonly String[] Events;
```

The event message names this component can raise, as offered to the editor's event pickers.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Flags

```csharp
public readonly EventMessageAttributeFlags Flags;
```

Flags controlling how and when the events above are discovered/propagated by the editor.

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

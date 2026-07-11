# AnimationEventMessage

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationEventMessage : IMessage
```

A Bang message dispatched when an animation frame fires a named event.

**Intent:** Lets gameplay systems react to specific frames of an animation (e.g., a footstep at frame 3, or a sword swing at frame 7) without polling.

**Use-case:** Listen for this message on entities with a sprite component; call `Is()` to check whether the event name matches the one your system cares about.

**Implements:** _[IMessage](../../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public AnimationEventMessage(string eventId)
```

Creates a message for the given event identifier string.

**Parameters** \
`eventId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### BroadcastedEvent
```csharp
public bool BroadcastedEvent { get; public set; }
```

This AnimationEvent is being broadcasted from another entity.
            Right now this is only for debug purposes.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Event
```csharp
public readonly string Event;
```

The identifier string of the animation event that was triggered.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### Is(ReadOnlySpan<T>)
```csharp
public bool Is(ReadOnlySpan<T> eventId)
```

Returns `true` if the event identifier matches `eventId`, using a case-insensitive comparison without allocating a string.

**Parameters** \
`eventId` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Is(string)
```csharp
public bool Is(string eventId)
```

Returns `true` if the event identifier matches `eventId` (case-insensitive string comparison).

**Parameters** \
`eventId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \



⚡
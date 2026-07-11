# MessagerAttribute

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public class MessagerAttribute : Attribute
```

Declares which [IMessage](../../Bang/Components/IMessage.html) types an [IMessagerSystem](../../Bang/Systems/IMessagerSystem.html) wants to
            receive. This is required for every system that implements [IMessagerSystem](../../Bang/Systems/IMessagerSystem.html) -
            [World](../../Bang/World.html) reads it to build the message
            watcher that routes matching messages to `IMessagerSystem.OnMessage`; in
            diagnostics mode, attaching this attribute to a system that is not an
            [IMessagerSystem](../../Bang/Systems/IMessagerSystem.html) is asserted against and silently dropped. Combine with
            [FilterAttribute](../../Bang/Systems/FilterAttribute.html) to further restrict which entities' messages are actually
            delivered to the system.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public MessagerAttribute(Type[] types)
```

Creates a new [MessagerAttribute](../../Bang/Systems/MessagerAttribute.html).

**Parameters** \
`types` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
#### Types
```csharp
public Type[] Types { get; }
```

The message types that will be dispatched to the owning [IMessagerSystem](../../Bang/Systems/IMessagerSystem.html).

**Returns** \
[Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \


⚡

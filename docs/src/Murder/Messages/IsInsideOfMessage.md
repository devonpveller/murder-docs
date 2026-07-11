# IsInsideOfMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct IsInsideOfMessage : IMessage
```

Sent to notify an entity that it is currently located inside another entity's trigger area, carrying the ID of the containing entity.

**Intent:** Inform a contained entity about which trigger or zone it is currently overlapping.

**Use-case:** Use this in area-of-effect or zone systems (such as water, fire, or safe zones) to notify entities within the area each frame, allowing them to apply environmental effects based on the zone type.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public IsInsideOfMessage(int insideOf)
```

**Parameters** \
`insideOf` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### InsideOf
```csharp
public readonly int InsideOf;
```

Entity ID of the trigger area or zone that this entity is currently inside.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
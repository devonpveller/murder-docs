# IsInsideOfMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct IsInsideOfMessage : IMessage
```

Sent to notify an entity that it is currently located inside another entity's trigger area, carrying the ID of the containing entity.

**Intent:** Inform a contained entity about which trigger or zone it is currently overlapping.

**Use-case:** No built-in engine system currently sends this message (it has no callers under `src/Murder`); it exists as a ready-made message type for game-specific area-of-effect or zone systems (such as water, fire, or safe zones) to notify entities within the area each frame, allowing them to apply environmental effects based on which zone entity they are inside of.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors

```csharp
public IsInsideOfMessage(int insideOf)
```

Creates a message identifying the trigger/zone entity that the receiving entity is currently inside of.

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

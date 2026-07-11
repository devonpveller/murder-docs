# DebugInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct DebugInteraction : IInteraction
```

Logs a message to the game console when the interaction fires.

**Intent:** Provides a simple diagnostic interaction for printing a custom log message during gameplay.

**Use-case:** Attach to an entity during development to verify that an interaction is being triggered, or to trace the sequence of events in a chain of interactions.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public DebugInteraction(string log)
```

**Parameters** \
`log` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Log
```csharp
public readonly string Log;
```
The message that will be printed to the game console when this interaction fires.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Prints `Log` to the game console via `GameLogger`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
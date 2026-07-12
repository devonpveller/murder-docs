# DebugInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct DebugInteraction : IInteraction
```

Prints a fixed message to the game log when the interaction fires.

**Intent:** Provides a simple diagnostic interaction for printing a custom log message during gameplay.

**Use-case:** Drop this in place of (or alongside) a real interaction while building or debugging an interaction chain in the level editor, to confirm that the trigger actually fires — and in what order — without needing to attach a debugger.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public DebugInteraction(string log)
```

Creates a debug interaction that will log `log` when triggered.

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

Prints `Log` to the game log via `GameLogger`. Ignores `world`, `interactor` and `interacted`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡

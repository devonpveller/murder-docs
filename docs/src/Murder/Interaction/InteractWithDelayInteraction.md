# InteractWithDelayInteraction

**Namespace:** Murder.Interaction \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractWithDelayInteraction : IInteraction
```

An interaction that waits a fixed number of seconds before invoking an inner `IInteraction`.

**Intent:** Delays the execution of any wrapped interaction by a configurable time, implemented as a coroutine so it does not block.

**Use-case:** Attach to a trigger entity when you want a door to open, a cutscene to begin, or an effect to fire after a short pause following player contact.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public InteractWithDelayInteraction()
```
Creates a new `InteractWithDelayInteraction` with default values (no delay, no inner interaction).

### ⭐ Properties
#### Interactive
```csharp
public readonly IInteraction Interactive;
```
The inner interaction that will be fired after `Time` seconds have elapsed.

**Returns** \
[IInteraction](../../Bang/Interactions/IInteraction.html) \
#### Time
```csharp
public readonly float Time;
```
Number of seconds to wait before invoking `Interactive`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Launches a coroutine that waits for `Time` seconds then calls `Interactive.Interact`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
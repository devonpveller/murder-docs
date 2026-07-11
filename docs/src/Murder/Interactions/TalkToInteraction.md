# TalkToInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct TalkToInteraction : IInteraction
```

Starts a dialogue sequence with the interacted entity by creating a dialogue child entity and setting its situation and state machine.

**Intent:** Initiates an NPC dialogue when the player interacts with a character.

**Use-case:** Attach to any character entity that has a `SituationComponent` to enable conversation when the player presses the interact button near it.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public TalkToInteraction()
```

### ⭐ Properties
#### DIALOGUE_CHILD
```csharp
public readonly static string DIALOGUE_CHILD;
```
The fixed child entity name used to store the active dialogue state machine entity under the NPC.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### CreateDialogueChild(World, Entity)
```csharp
public Entity CreateDialogueChild(World world, Entity interacted)
```
Creates (or reuses) the dialogue child entity under the interacted entity; returns `null` if a dialogue is already in progress.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Creates the dialogue child entity and starts the `DialogStateMachine` for the current situation.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
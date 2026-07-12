# TalkToInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct TalkToInteraction : IInteraction
```

Starts (or resumes) a dialogue with the interacted entity by creating a dedicated dialogue child entity and starting a `DialogStateMachine` on it for the character's current situation.

**Intent:** Initiates an NPC dialogue when the player (or another entity) interacts with a character.

**Use-case:** Attach to any character entity that also carries a `SituationComponent` (required — the type is decorated with `[Requires(typeof(SituationComponent))]`) to enable conversation when the player presses the interact button near it. Because the running dialogue lives on a separate child entity named `DialogueChild`, repeated interactions while a conversation is already in progress are safely ignored instead of restarting it.

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

The fixed child entity name under which the active dialogue's state machine entity is stored on the NPC. Used both to detect whether a dialogue is already running and to look it up later via `TryFetchDialogueChild`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### CreateDialogueChild(World, Entity)

```csharp
public static Entity CreateDialogueChild(World world, Entity interacted)
```

Creates (or reuses) the `DIALOGUE_CHILD` entity under `interacted` that will host the running `DialogStateMachine`. Returns `null` when a dialogue is already in progress (the existing child already has a state machine), so callers can treat that as a no-op rather than restarting the conversation. Also returns `null`, after logging an error, when `interacted` is `null`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Resolves `interacted`'s current `SituationComponent` (preferring an active override situation, if one is set, over the default situation), creates or reuses its dialogue child entity via `CreateDialogueChild`, propagates the interactor's `SpeakerComponent` and its "automatic next dialogue" flag to the child if applicable, then starts a `DialogStateMachine` on it for the resolved situation. Logs an error and does nothing if `interacted` is `null`, or if it has no situation to run.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

#### TryFetchDialogueChild(Entity)

```csharp
public static Entity TryFetchDialogueChild(Entity interacted)
```

Looks up the dialogue child entity (named `DIALOGUE_CHILD`) previously created for `interacted` by `CreateDialogueChild`, if one exists.

**Parameters** \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

⚡

# DialogueServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class DialogueServices
```

Helpers for querying, previewing, and creating dialogue/character-runtime state from `SituationComponent` data, and for firing generic `IInteractiveComponent` interactions.

**Intent:** Centralizes the logic for turning a `Guid` character asset plus a situation string into a runnable `CharacterRuntime`, and for probing that runtime (does it have dialogue? what's the first/all lines?) without callers needing to understand the character/blackboard/situation plumbing.

**Use-case:** Use `HasDialogue`/`HasNewDialogue` to decide whether to show a dialogue prompt indicator above an NPC (the latter distinguishes "has anything to say" from "has something the player hasn't seen yet"). Use `FetchFirstLine` to preview the opening line in UI without starting the full conversation, or `FetchAllLines`/`FetchAllLinesSeparatedBy` to dump every line of a situation (e.g. for tooltips, logs, or localization tooling). Use `SetOverrideSituation`/`RemoveOverrideSituation` when some system (cutscene, quest, ability) needs to temporarily override what an entity says, layered by `SituationOrigin`. `Fire` is a small dispatch helper for running a batch of `IInteractiveComponent` actions against an interactor/interacted pair.

### ⭐ Methods

#### CreateCharacterFrom(Guid, string)

```csharp
public static CharacterRuntime? CreateCharacterFrom(Guid character, string? situation)
```

Creates a `CharacterRuntime` for the given character asset and situation name, seeded from the active save's `BlackboardTracker`. Returns `null` if `situation` is `null` or the character can't be resolved from the save data. This is the common entry point used by every other method on this class before they can query or advance dialogue.

**Parameters** \
`character` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`situation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[CharacterRuntime](../../Murder/Core/Dialogs/CharacterRuntime.html) \

#### CreateLine(Line)

```csharp
public static LineComponent CreateLine(Line line)
```

Wraps a raw `Line` value in a `LineComponent`, timestamped with the current unscaled game time. Used when spawning a speech-bubble/line-display entity from dialogue data.

**Parameters** \
`line` [Line](../../Murder/Core/Dialogs/Line.html) \

**Returns** \
[LineComponent](../../Murder/Components/LineComponent.html) \

#### FetchAllLines(World, Entity, SituationComponent)

```csharp
public static Line[] FetchAllLines(World? world, Entity? target, SituationComponent situation)
```

Advances through the entire dialogue situation via `CharacterRuntime.NextLine`, collecting every text `Line` encountered. Stops (with a warning logged) as soon as it hits a `ChoiceLine`, since choice branching isn't supported for "fetch everything" traversal. Returns an empty array if the character/situation can't be resolved. Useful for exporting or previewing the full linear content of a situation, e.g. tooling or localization review.

**Parameters** \
`world` [World](../../Bang/World.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \

**Returns** \
[Line[]](../../Murder/Core/Dialogs/Line.html) \

#### FetchAllLinesSeparatedBy(World, Entity, SituationComponent, string)

```csharp
public static string FetchAllLinesSeparatedBy(World? world, Entity? target, SituationComponent situation, string separator)
```

Calls `FetchAllLines` and joins the localized text of every text line with `separator`, skipping non-text lines. Useful for building a single preview/summary string of a situation's dialogue (e.g. for an editor inspector or a debug overlay) without having to iterate the array yourself.

**Parameters** \
`world` [World](../../Bang/World.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \
`separator` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FetchFirstLine(World, Entity, SituationComponent)

```csharp
public static string FetchFirstLine(World? world, Entity? target, SituationComponent situation)
```

Returns the localized text of the first dialogue line the situation would show, or an empty string if the situation has no character (`Guid.Empty`), can't be resolved, or its first entry is a choice rather than text. Intended for lightweight previews (e.g. a UI hint showing what an NPC is about to say) without mutating any dialogue progress state.

**Parameters** \
`world` [World](../../Bang/World.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### HasDialogue(World, Entity, SituationComponent)

```csharp
public static bool HasDialogue(World world, Entity? e, SituationComponent situation)
```

Returns `true` if `situation` is non-empty and its character has at least one dialogue line available to show (regardless of whether the player has already seen it). Use this to decide whether an NPC should display any "talk to me" indicator at all.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasNewDialogue(World, Entity, SituationComponent)

```csharp
public static bool HasNewDialogue(World world, Entity? e, SituationComponent situation)
```

Returns `true` if `situation` is non-empty and its character has *unseen* dialogue content available (checked with `checkForNewContentOnly: true`), as opposed to `HasDialogue` which also counts already-seen lines. Use this for a "new dialogue available" marker (e.g. an exclamation icon) that should disappear once the player has heard everything once.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetPortraitName(SpeakerAsset, string, string)

```csharp
public static string GetPortraitName(SpeakerAsset speaker, string? portrait, string? fallback = null)
```

Resolves which portrait name should be used for a line: returns `portrait` if given, otherwise `fallback` if given, otherwise the speaker's `DefaultPortrait`, otherwise the first key in `speaker.Portraits`, otherwise the literal string `"Idle"`. Centralizes this fallback chain so dialogue-rendering code doesn't need to reimplement it every time it needs to pick a portrait sprite for a line.

**Parameters** \
`speaker` [SpeakerAsset](../../Murder/Assets/SpeakerAsset.html) \
`portrait` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`fallback` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SetOverrideSituation(Entity, SituationOrigin, SituationComponent)

```csharp
public static void SetOverrideSituation(this Entity e, SituationOrigin origin, SituationComponent situation)
```

Sets or updates the entity's `OverrideSituationComponent` so that the situation registered under `origin` is `situation`. Multiple systems can each own their own `origin` slot (e.g. a quest system vs. a cutscene system) without clobbering each other's overrides. Use this to make an entity temporarily say/do something other than its default dialogue situation — for example, an NPC that has special dialogue during an active quest step.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`origin` [SituationOrigin](../../Murder/Components/Dialogs/OverrideSituationComponent.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \

#### RemoveOverrideSituation(Entity, SituationOrigin)

```csharp
public static void RemoveOverrideSituation(this Entity e, SituationOrigin origin)
```

Removes the override registered under `origin` from the entity's `OverrideSituationComponent`. If that was the last remaining override, the component itself is removed from the entity; otherwise the component is updated to drop just that origin's entry. Call this to hand dialogue control back to the entity's default situation once the system that set the override (quest, cutscene, etc.) is done with it.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`origin` [SituationOrigin](../../Murder/Components/Dialogs/OverrideSituationComponent.html) \

#### Fire(World, Entity, Entity, ImmutableArray&lt;IInteractiveComponent&gt;)

```csharp
public static void Fire(World world, Entity interactor, Entity? interacted, ImmutableArray<IInteractiveComponent> actions)
```

Calls `Interact(world, interactor, interacted)` on every component in `actions`, in order. This is a small dispatch helper used to run a batch of interaction effects (which may or may not be dialogue-related) together, such as everything attached to an interaction/trigger entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \
`actions` [ImmutableArray\<IInteractiveComponent\>](../../Bang/Interactions/IInteractiveComponent.html) \

⚡

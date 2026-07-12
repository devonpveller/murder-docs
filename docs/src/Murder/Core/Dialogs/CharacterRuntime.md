# CharacterRuntime

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public class CharacterRuntime
```

Maintains the live playback state for a character's dialogue: the active situation, current dialog node, and active line index.

**Intent:** Drives a character's dialogue session at runtime — advancing through dialog nodes, evaluating blackboard conditions, resolving the next displayable line, and committing choices.

**Use-case:** Instantiate with a `Character` and a starting situation name; call `HasNext` each frame to check whether dialogue remains, `NextLine` to retrieve the next displayable line, and `DoChoice` to commit a player-selected option.

### ⭐ Constructors

```csharp
public CharacterRuntime(Character character, string situation)
```

Creates a new runtime for the given character, immediately starting playback at the situation with the given name.

**Parameters** \
`character` [Character](../../../Murder/Core/Dialogs/Character.html) \
`situation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### CheckRequirements(World, ImmutableArray<T>, out Int32&)

```csharp
public bool CheckRequirements(World world, ImmutableArray<T> requirements, Int32& score)
```

Evaluates a set of `CriterionNode` requirements against the current world state and returns whether they pass, writing the match score into `score`.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`requirements` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`score` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasContentOnNextDialogueLine(World, Entity, bool)

```csharp
public bool HasContentOnNextDialogueLine(World world, Entity target, bool checkForNewContentOnly)
```

Returns whether the upcoming dialogue node contains at least one displayable line, without consuming it (unlike `NextLine`, this does not advance playback). Skips over empty exit nodes and, when `checkForNewContentOnly` is `true`, also requires that the node has never been played before. Useful for deciding whether to show an "interact" prompt over an NPC before the player commits to starting the conversation.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`target` [Entity](../../../Bang/Entities/Entity.html) \
`checkForNewContentOnly` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasNext(World, Entity, bool)

```csharp
public bool HasNext(World world, Entity target, bool track)
```

Returns whether the active dialog state for this dialogue is valid or not.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`target` [Entity](../../../Bang/Entities/Entity.html) \
`track` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### NextLine(World, Entity)

```csharp
public T? NextLine(World world, Entity target)
```

Advances the dialogue and returns the next `DialogLine` to display (either a `Line` or a `ChoiceLine`), or `null` when the conversation is over. As a side effect, this also fires any `Dialog.Actions` attached to nodes it passes through, plays line sounds, and records play counts in `BlackboardTracker`.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`target` [Entity](../../../Bang/Entities/Entity.html) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### DoChoice(int, World, Entity)

```csharp
public void DoChoice(int choice, World world, Entity target)
```

Commits the player's selected choice by index (matching the order of `ChoiceLine.Choices` returned from the preceding `NextLine` call), plays the chosen option's sound, and advances the dialogue to the resulting branch, executing any actions along the way.

**Parameters** \
`choice` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`world` [World](../../../Bang/World.html) \
`target` [Entity](../../../Bang/Entities/Entity.html) \

#### StartAtSituation(string)

```csharp
public void StartAtSituation(string situation)
```

Resets the playback cursor (current dialog and active line) and begins the dialogue from the `Situation` with the given name. If no such situation exists on the character, logs an error and leaves the runtime with no dialogue available.

**Parameters** \
`situation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

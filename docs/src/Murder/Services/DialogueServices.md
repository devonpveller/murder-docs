# DialogueServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class DialogueServices
```

Helpers for querying and creating dialogue state from character assets and situation components.

**Intent:** Provides utilities for checking whether an entity has dialogue available and for constructing runtime dialogue objects.

**Use-case:** Use `HasDialogue` to decide whether to show a dialogue prompt indicator above an NPC, or `FetchFirstLine` to display a preview of the opening line in UI without starting the full conversation.

### ⭐ Methods
#### HasDialogue(World, Entity, SituationComponent)
```csharp
public bool HasDialogue(World world, Entity e, SituationComponent situation)
```
Returns `true` if the character has at least one dialogue line available for the given situation.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasNewDialogue(World, Entity, SituationComponent)
```csharp
public bool HasNewDialogue(World world, Entity e, SituationComponent situation)
```
Returns `true` if the character has unseen dialogue available for the given situation.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CreateCharacterFrom(Guid, int)
```csharp
public CharacterRuntime CreateCharacterFrom(Guid character, int situation)
```
Creates a `CharacterRuntime` for the given character asset and situation index, initialised from the active save's blackboard.

**Parameters** \
`character` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`situation` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[CharacterRuntime](../../Murder/Core/Dialogs/CharacterRuntime.html) \

#### FetchAllLines(World, Entity, SituationComponent)
```csharp
public Line[] FetchAllLines(World world, Entity target, SituationComponent situation)
```
Advances through the entire dialogue situation and returns all text lines that would be spoken.

**Parameters** \
`world` [World](../../Bang/World.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \

**Returns** \
[Line[]](../../Murder/Core/Dialogs/Line.html) \

#### CreateLine(Line)
```csharp
public LineComponent CreateLine(Line line)
```
Wrap a raw `Line` value in a `LineComponent` timestamped to the current unscaled game time.

**Parameters** \
`line` [Line](../../Murder/Core/Dialogs/Line.html) \

**Returns** \
[LineComponent](../../Murder/Components/LineComponent.html) \

#### FetchFirstLine(World, Entity, SituationComponent)
```csharp
public string FetchFirstLine(World world, Entity target, SituationComponent situation)
```
Returns the localized text of the first dialogue line in the situation, or an empty string if none exists.

**Parameters** \
`world` [World](../../Bang/World.html) \
`target` [Entity](../../Bang/Entities/Entity.html) \
`situation` [SituationComponent](../../Murder/Components/SituationComponent.html) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡
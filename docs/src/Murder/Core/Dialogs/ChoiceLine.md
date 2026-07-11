# ChoiceLine

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct ChoiceLine
```

A displayable dialogue line that presents the player with a set of selectable options.

**Intent:** Carries all the information needed to render a choice prompt — the speaking character, portrait, a title or question text, and the ordered list of choice labels.

**Use-case:** Returned by `CharacterRuntime.NextLine` (wrapped in a `DialogLine`) when the active dialog node is a choice block; read `Choices` to populate your UI option list and call `CharacterRuntime.DoChoice` with the player's index.

### ⭐ Constructors
```csharp
public ChoiceLine(Guid speaker, string portrait, string title, ImmutableArray<T> choices)
```

Creates a choice line with the given speaker, portrait, title text, and list of option labels.

**Parameters** \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`portrait` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`title` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`choices` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### Choices
```csharp
public readonly ImmutableArray<T> Choices;
```

Choices available to the player to pick.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Portrait
```csharp
public readonly string Portrait;
```

Optional portrait key for the speaking character to display alongside the choice prompt; `null` means use the speaker's default portrait.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Speaker
```csharp
public readonly T? Speaker;
```

GUID of the `SpeakerAsset` presenting this choice; `null` when no speaker is associated.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Title
```csharp
public readonly string Title;
```

Dialog title.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡
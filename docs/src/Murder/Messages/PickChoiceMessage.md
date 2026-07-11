# PickChoiceMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct PickChoiceMessage : IMessage
```

Carries the player's selection (or cancellation) from a dialogue choice prompt.

**Intent:** Communicate the result of a player-facing dialogue choice menu back to the dialogue system.

**Use-case:** Send this from the UI system when the player selects an option or presses cancel in a dialogue choice menu. The dialogue state machine receives it to branch the conversation or close the dialogue if cancelled.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public PickChoiceMessage(bool cancel)
```

Creates a message indicating the choice prompt was cancelled without selecting an option.

**Parameters** \
`cancel` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public PickChoiceMessage(int choice)
```

Creates a message with the zero-based index of the option the player selected.

**Parameters** \
`choice` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Choice
```csharp
public readonly int Choice;
```

Zero-based index of the dialogue option selected by the player.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### IsCancel
```csharp
public readonly bool IsCancel;
```

Whether the player cancelled the choice prompt without making a selection.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \


⚡
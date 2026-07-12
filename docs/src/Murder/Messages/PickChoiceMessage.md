# PickChoiceMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct PickChoiceMessage : IMessage
```

Carries the player's selection (or cancellation) from a dialogue choice prompt.

**Intent:** Communicate the result of a player-facing dialogue choice menu back to the dialogue system.

**Use-case:** `DialogStateMachine.Talk()` publishes a `ChoiceComponent` on the dialogue entity and suspends with `Wait.ForMessage<PickChoiceMessage>()`. Send this message to that entity from UI/input code once the player selects an option (or cancels) in a dialogue choice menu; `DialogStateMachine.OnMessage` captures `Choice` from it so `Talk()` can read it back after resuming and call `CharacterRuntime.DoChoice(choiceIndex, ...)` to branch the conversation.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors

```csharp
public PickChoiceMessage(bool cancel)
```

Creates a message carrying only whether the choice prompt was cancelled, leaving `Choice` at its default of `0`. Pass `true` when the player backs out of the choice menu without picking an option.

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

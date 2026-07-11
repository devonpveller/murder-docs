# ChoiceComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct ChoiceComponent : IComponent
```

Holds the current dialogue choice presented to the player during a conversation.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Carries the `ChoiceLine` data that the UI system needs to display a multiple-choice dialogue prompt.

**Use-case:** Added to the unique dialogue entity by the dialogue system when a branching choice is reached; the choice UI reads this component and removes it once the player selects an option.

### ⭐ Constructors
```csharp
public ChoiceComponent(ChoiceLine choice)
```

**Parameters** \
`choice` [ChoiceLine](../../Murder/Core/Dialogs/ChoiceLine.html) \

### ⭐ Properties
#### Choice
```csharp
public readonly ChoiceLine Choice;
```

The choice data to present to the player, including the available option lines.

**Returns** \
[ChoiceLine](../../Murder/Core/Dialogs/ChoiceLine.html) \


⚡
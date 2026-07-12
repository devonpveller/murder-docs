# AutomaticNextDialogueComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AutomaticNextDialogueComponent : IComponent
```

Marker component flagging a dialogue interaction as auto-advancing rather than waiting on player confirmation.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Lets an interactable entity (e.g. an NPC or sign) mark its conversations as auto-advancing. `TalkToInteraction.Interact` checks for this component on the interacted entity and, if present, propagates it onto the dialogue entity it creates. `DialogStateMachine.Talk` then checks it on the dialogue entity and, if present, attaches `DoNotPauseComponent` so the auto-advancing conversation keeps progressing even while the game is paused. The actual "don't wait for a confirm button" behavior for reading each line is implemented by the game's own dialogue UI/box, which is expected to check for this component and skip its normal wait-for-input step.

**Use-case:** Attach to an interactable entity (the one with `TalkToInteraction`/`SituationComponent`) for NPC monologue sequences, ambient chatter, or tutorial text that should play through on its own timing instead of requiring the player to press a button after every line.

⚡

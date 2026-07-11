# AutomaticNextDialogueComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AutomaticNextDialogueComponent : IComponent
```

Marker component that instructs the dialogue system to advance to the next dialogue line automatically without waiting for player input.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Skips the usual "wait for player confirmation" step so dialogue progresses on its own timing.

**Use-case:** Attach to a dialogue entity for NPC monologue sequences or tutorial text that should auto-advance after a timed delay or animation event.



⚡
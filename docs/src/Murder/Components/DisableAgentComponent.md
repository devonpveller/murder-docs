# DisableAgentComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DisableAgentComponent : IComponent
```

Disables the agent from using the AgentMover and other agent related systems

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Pauses all agent movement and AI processing without removing the agent's configuration data.

**Use-case:** Attach during cutscenes, dialogue, or stun effects to freeze an entity in place; remove the component to resume normal agent behavior.

### ⭐ Constructors
```csharp
public DisableAgentComponent()
```



⚡
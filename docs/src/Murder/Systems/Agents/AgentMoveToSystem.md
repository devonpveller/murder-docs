# AgentMoveToSystem

**Namespace:** Murder.Systems.Agents \
**Assembly:** Murder.dll

```csharp
public class AgentMoveToSystem : IFixedUpdateSystem, ISystem
```

Simple system for moving agents to another position. Looks for 'MoveTo' components and adds agent inpulses to it.

**Intent:** Moves agent entities toward their `MoveToComponent` target by applying velocity impulses.

**Use-case:** Include in worlds where NPCs or player characters navigate to positions set via `MoveToComponent`.

**Implements:** _[IFixedUpdateSystem](../../../Bang/Systems/IFixedUpdateSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public AgentMoveToSystem()
```

### ⭐ Methods
#### FixedUpdate(Context)
```csharp
public virtual void FixedUpdate(Context context)
```

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡
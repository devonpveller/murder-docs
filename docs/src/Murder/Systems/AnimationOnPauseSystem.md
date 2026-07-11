# AnimationOnPauseSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class AnimationOnPauseSystem : IUpdateSystem, ISystem
```

System that will automatically completes aseprites on a freeze cutscene.

**Intent:** Forces all sprite and agent-sprite animations to complete when the world is in a freeze-cutscene state.

**Use-case:** Ensures that cutscene-frozen animations reach their final frame so gameplay events that depend on animation completion can fire and the scene can proceed.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public AnimationOnPauseSystem()
```

### ⭐ Methods
#### Update(Context)
```csharp
public virtual void Update(Context context)
```

Checks whether the world is currently skipping delta time (freeze-cutscene mode) and sends animation-complete messages to all sprite and agent-sprite entities.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡
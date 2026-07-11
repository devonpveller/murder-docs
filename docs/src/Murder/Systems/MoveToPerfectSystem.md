# MoveToPerfectSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class MoveToPerfectSystem : IFixedUpdateSystem, ISystem
```

Simple system for moving agents to another position. Looks for 'MoveTo' components and adds agent inpulses to it.

**Intent:** Provides precise, eased movement from a start position to a target for entities that should not use velocity-based physics.

**Use-case:** Add `MoveToPerfectComponent` to UI elements, cutscene actors, or scripted objects that need to glide smoothly to a destination with a configurable easing curve.

**Implements:** _[IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public MoveToPerfectSystem()
```

### ⭐ Methods
#### FixedUpdate(Context)
```csharp
public virtual void FixedUpdate(Context context)
```

Evaluates the easing curve at the current elapsed time and snaps the entity's position along the interpolated path; optionally separates from nearby actor entities.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡
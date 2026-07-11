# ISoundBlackboard

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public abstract class ISoundBlackboard : IBlackboard
```

This tracks and listens to parameters relevant to music and sound.

**Intent:** Marks a blackboard as sound-scoped so the engine routes its facts to the audio parameter store rather than the gameplay or character stores.

**Use-case:** Extend this class when creating a blackboard whose facts drive FMOD parameters or other adaptive audio systems; annotate it with `[Blackboard]` as usual.

**Implements:** _[IBlackboard](../../../Murder/Core/Dialogs/IBlackboard.html)_

### ⭐ Constructors
```csharp
protected ISoundBlackboard()
```

Protected constructor for subclasses.

### ⭐ Properties
#### Kind
```csharp
public virtual BlackboardKind Kind { get; }
```

Always returns `BlackboardKind.Sound` for sound-parameter blackboards.

**Returns** \
[BlackboardKind](../../../Murder/Core/Dialogs/BlackboardKind.html) \


⚡
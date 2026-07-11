# DestroyOnAnimationCompleteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DestroyOnAnimationCompleteComponent : IComponent
```

Instructs the engine to destroy (or deactivate) this entity when its sprite animation finishes.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Automates the lifetime of one-shot animation effects so they clean themselves up without manual teardown logic.

**Use-case:** Attach to particle bursts, hit-flash sprites, or other temporary effects; the system watching for `AnimationCompleteComponent` will then destroy or deactivate the entity accordingly.

### ⭐ Constructors
```csharp
public DestroyOnAnimationCompleteComponent()
```

```csharp
public DestroyOnAnimationCompleteComponent(bool deactivateOnComplete)
```

**Parameters** \
`deactivateOnComplete` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### DeactivateOnComplete
```csharp
public readonly bool DeactivateOnComplete;
```

Whether it should deactivate instead of destroying.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \


⚡
# FlashSpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FlashSpriteComponent : IComponent
```

Causes the entity's sprite to flash (rapidly blink) for a limited duration, typically used as hit or damage feedback.

**Intent:** Visually indicate that an entity was hit or received feedback by making its sprite blink on and off until a timer expires.

**Use-case:** Attach at runtime (e.g. on damage taken) and pass the desired end time via the constructor; the flash system removes the component automatically when `DestroyAtTime` is reached.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public FlashSpriteComponent(float destroyTimer)
```

**Parameters** \
`destroyTimer` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### DestroyAtTime
```csharp
public readonly float DestroyAtTime;
```

Absolute game time (in seconds) at which the flash effect ends and this component is removed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡
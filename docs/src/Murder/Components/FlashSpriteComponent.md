# FlashSpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FlashSpriteComponent : IComponent
```

Marks an entity's sprite to flash for a short duration, typically used as damage/hit feedback. Rendering systems check for this component to draw the sprite with a flash overlay, and `SpriteFlashCleanupSystem` removes it once `DestroyAtTime` is reached. Runtime-only: never persisted to save files or serialized assets.

**Intent:** Visually indicate that an entity was hit or received feedback by flashing its sprite for a fixed window of game time, without the caller needing to track and clear a timer manually — the cleanup system does that automatically.

**Use-case:** Attach at runtime (e.g. when an entity takes damage), passing the absolute game time at which the flash should end, such as `Game.Now + 0.2f`; `SpriteFlashCleanupSystem` removes the component on its own once `Game.Now` passes `DestroyAtTime`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public FlashSpriteComponent(float destroyTimer)
```

Creates a flash effect that lasts until `destroyTimer`.

**Parameters** \
`destroyTimer` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### DestroyAtTime

```csharp
public readonly float DestroyAtTime;
```

The absolute game time (`Game.Now`) at which the flash effect ends and this component is automatically removed by `SpriteFlashCleanupSystem`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

# DestroyOnAnimationCompleteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DestroyOnAnimationCompleteComponent : IComponent
```

Instructs the engine to clean up this entity — destroying it, deactivating it, or otherwise tearing down its visuals — once its current sprite animation finishes playing.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Automates the lifetime of one-shot animation effects (explosions, hit-flashes, death animations) so they clean themselves up the moment their animation completes, without a bespoke system per effect type.

**Use-case:** Attach to particle bursts, hit-flash sprites, or death/despawn animations. `DestroyOnAnimationCompleteSystem` listens for `AnimationCompleteMessage` (only reacting when the completed animation's `CompleteStyle` is `Sequence`, i.e. it is not looping) and, once the entity's `SpriteComponent` has no further queued `NextAnimations`, applies whichever `Settings` flag was configured — destroying the entity, deactivating it, removing its solid collider, zeroing its alpha, removing its sprite, or doing nothing.

### ⭐ Constructors

```csharp
public DestroyOnAnimationCompleteComponent()
```

Creates the component with the default behavior: `Settings` is `DestroyOnAnimationCompleteFlags.Destroy`, `ChangeSpriteBatchOnComplete` is unset, and `KeepComponentAfterTriggered` is `false`. Equivalent to attaching a plain "destroy me when done animating" marker.

```csharp
public DestroyOnAnimationCompleteComponent(DestroyOnAnimationCompleteFlags settings)
```

Creates the component with an explicit removal behavior, e.g. `Deactivate` to hide the entity instead of destroying it, or `None` to only trigger the sprite-batch change without removing anything.

**Parameters** \
`settings` [DestroyOnAnimationCompleteFlags](../../Murder/Components/DestroyOnAnimationCompleteFlags.html) \

```csharp
public DestroyOnAnimationCompleteComponent(DestroyOnAnimationCompleteFlags settings, int? changeSpriteBatch)
```

Creates the component with both an explicit removal behavior and a sprite batch to move the entity's sprite into right before that behavior is applied. Useful for effects that need to render in a different batch (e.g. a foreground overlay) during their final frame.

**Parameters** \
`settings` [DestroyOnAnimationCompleteFlags](../../Murder/Components/DestroyOnAnimationCompleteFlags.html) \
`changeSpriteBatch` [int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

### ⭐ Properties

#### ChangeSpriteBatchOnComplete

```csharp
public int? ChangeSpriteBatchOnComplete { get; public set; }
```

Optional [Batches2D](../../Murder/Core/Graphics/Batches2D.html) index that the entity's `SpriteComponent` is moved into right before the `Settings` action is applied. Left `null` (the default) to leave the sprite in its current batch.

**Returns** \
[int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### KeepComponentAfterTriggered

```csharp
public readonly bool KeepComponentAfterTriggered;
```

When `true`, this component is left on the entity after it fires instead of being removed. Set this if the same entity can raise multiple `AnimationCompleteMessage` events and should re-trigger the configured behavior each time (for example, a looping hit-flash that deactivates every time its flash animation ends).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Settings

```csharp
public readonly DestroyOnAnimationCompleteFlags Settings;
```

Determines what happens to the entity when its animation completes: fully destroy it, deactivate it, remove its solid collider, zero its alpha, remove its sprite/highlight, or do nothing. Defaults to `DestroyOnAnimationCompleteFlags.Destroy`.

**Returns** \
[DestroyOnAnimationCompleteFlags](../../Murder/Components/DestroyOnAnimationCompleteFlags.html) \

⚡

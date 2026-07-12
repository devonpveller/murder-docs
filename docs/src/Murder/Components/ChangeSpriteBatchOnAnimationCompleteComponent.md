# ChangeSpriteBatchOnAnimationCompleteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct ChangeSpriteBatchOnAnimationCompleteComponent : IComponent
```

One-shot request to move an entity's sprite to a different sprite batch as soon as its current animation finishes.

**Intent:** Some effects need to render in one batch while an animation plays (e.g. an additive/foreground batch for a flashy intro) and then settle into the normal gameplay batch once it's done, without a system having to poll the animation state every frame. `ChangeSpriteBatchOnAnimationCompleteSystem` listens for `AnimationCompleteMessage` and, when the message matches this component's `OnCompleteStyle`, sets the entity's `SpriteComponent.TargetSpriteBatch` to `SpriteBatch` and removes this component so the change only ever happens once.

**Use-case:** Add to an entity whose sprite should switch sprite batches automatically after its animation completes — for example, a scripted introduction animation drawn in a special batch that should drop back into the normal gameplay batch once it finishes playing.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public ChangeSpriteBatchOnAnimationCompleteComponent()
```

Creates a request targeting sprite batch 0, triggered when a full animation sequence completes (`AnimationCompleteStyle.Sequence`).

```csharp
public ChangeSpriteBatchOnAnimationCompleteComponent(int spriteBatch, AnimationCompleteStyle onCompleteStyle)
```

**Parameters** \
`spriteBatch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`onCompleteStyle` [AnimationCompleteStyle](../../Murder/Messages/AnimationCompleteStyle.html) \

### ⭐ Properties

#### OnCompleteStyle

```csharp
public readonly AnimationCompleteStyle OnCompleteStyle;
```

Which kind of animation-complete event should trigger the batch change. `Single` triggers on the very next `AnimationCompleteMessage` regardless of that message's own style; `Sequence` only triggers when the message's style is also `Sequence` (a full multi-step animation sequence finishing, not just one step of it).

**Returns** \
[AnimationCompleteStyle](../../Murder/Messages/AnimationCompleteStyle.html) \

#### SpriteBatch

```csharp
public readonly int SpriteBatch;
```

Index of the sprite batch (see [Batches2D](../../Murder/Core/Graphics/Batches2D.html)) to move the entity's sprite into once the animation completes.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

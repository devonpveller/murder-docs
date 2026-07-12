# AnimationCompleteMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationCompleteMessage : IMessage
```

Sent by the sprite rendering code whenever a playing animation reaches its end, carrying an [AnimationCompleteStyle](../../Murder/Messages/AnimationCompleteStyle.html) that tells listeners whether this was just one step of a longer chain or the very end of the whole sequence.

**Intent:** Let systems and components react to "this entity just finished animating" without polling sprite state every frame, while still letting them tell the difference between an intermediate loop/step and the true end of a chained/queued animation.

**Use-case:** `RenderServices` sends this message from several call sites (finishing an `AnimationOverloadComponent` override, chaining to the next queued sprite animation, or completing a non-looping animation) so gameplay code never has to send it manually. Listen for it with `[Messager(typeof(AnimationCompleteMessage))]` — for example `DestroyOnAnimationCompleteSystem` uses it to destroy/deactivate/fade an entity once its death or intro animation truly ends (checking `CompleteStyle == AnimationCompleteStyle.Sequence`), and `ChangeSpriteBatchOnAnimationCompleteSystem` uses it to move a `ChangeSpriteBatchOnAnimationCompleteComponent` entity into a different sprite batch once its configured style matches.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors

```csharp
public AnimationCompleteMessage(AnimationCompleteStyle style)
```

Creates the message with the style describing which kind of completion just happened. This is what the source-generated `entity.SendAnimationCompleteMessage(...)` extension constructs internally when a system reports that an entity's animation has finished.

**Parameters** \
`style` [AnimationCompleteStyle](../../Murder/Messages/AnimationCompleteStyle.html) \

### ⭐ Properties

#### CompleteStyle

```csharp
public readonly AnimationCompleteStyle CompleteStyle;
```

Distinguishes a single-step completion (`Single`, e.g. one non-looping animation in a queue just ended but more remain) from a full-sequence completion (`Sequence`, e.g. the last queued/chained animation, or a non-looping `AnimationOverloadComponent`, finished). Listeners typically only care about `Sequence` when they want to trigger "the animation is truly over" logic.

**Returns** \
[AnimationCompleteStyle](../../Murder/Messages/AnimationCompleteStyle.html) \

⚡

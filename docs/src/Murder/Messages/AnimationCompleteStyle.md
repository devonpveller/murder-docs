# AnimationCompleteStyle

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed enum AnimationCompleteStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Distinguishes the two kinds of "animation finished" event carried by [AnimationCompleteMessage](../../Murder/Messages/AnimationCompleteMessage.html): a single step inside a longer queue/chain versus the true end of the whole sequence.

**Intent:** Give listeners of `AnimationCompleteMessage` enough information to tell an intermediate completion (e.g. one non-looping animation in a multi-animation queue finished, but more are still coming) apart from a final one (e.g. the last queued animation finished, or a non-looping `AnimationOverloadComponent` completed), so they only react when the whole thing is actually over.

**Use-case:** Compare against `AnimationCompleteMessage.CompleteStyle` inside an `[Messager(typeof(AnimationCompleteMessage))]` system. `DestroyOnAnimationCompleteSystem` only proceeds with destruction/deactivation when the style is `Sequence`, so it doesn't act prematurely on an intermediate step of a chained animation. `ChangeSpriteBatchOnAnimationCompleteComponent.OnCompleteStyle` uses the same enum to let content authors choose whether a sprite-batch swap should happen on any completion (`Single`) or only once the full sequence ends (`Sequence`).

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Single

```csharp
public static const AnimationCompleteStyle Single;
```

One step of a queued/chained animation just finished (for example one non-looping animation in a `NextAnimations` queue), but the queue or chain is not necessarily done yet.

**Returns** \
[AnimationCompleteStyle](../../Murder/Messages/AnimationCompleteStyle.html) \

#### Sequence

```csharp
public static const AnimationCompleteStyle Sequence;
```

The entire animation sequence has finished — either the last queued/chained animation played out, or a non-looping `AnimationOverloadComponent` completed and was removed. Systems that should only fire once "everything is done" (such as destroying an entity) check for this value.

**Returns** \
[AnimationCompleteStyle](../../Murder/Messages/AnimationCompleteStyle.html) \

⚡

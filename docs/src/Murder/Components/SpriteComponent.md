# SpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteComponent : IComponent
```

Primary rendering component for Aseprite-based sprites. Stores the animation asset reference, the queue of animations to play, the render offset, Y-sort value, and related display options.

**Intent:** Drive sprite rendering and animation playback for any entity that displays an Aseprite sprite.

**Use-case:** Attach to any game-world entity that should render a sprite; set `AnimationGuid` to the target `SpriteAsset`, populate `NextAnimations` with the desired animation sequence (via a constructor or one of the `Play`/`PlayAfter` "with"-style methods), and let `SpriteRenderSystem` handle drawing. `SpriteRenderSystem` reads `CurrentAnimation` (the first entry of `NextAnimations`) each frame to pick the frame to draw, applies `Offset` and `TargetSpriteBatch`, rotates the sprite when `RotateWithFacing` is set and the entity has a `FacingComponent`, and draws the `HighlightStyle` outline when the entity is selected/highlighted. Requires a `PositionComponent` (`[Requires(typeof(PositionComponent))]`).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SpriteComponent()
```

Default constructor used by the ECS/serializer. Produces an empty sprite (`AnimationGuid` is `Guid.Empty`, `NextAnimations` is empty) that must be configured before anything is drawn.

```csharp
public SpriteComponent(Guid guid)
```

Convenience constructor that only sets `AnimationGuid`, leaving offset, animation queue, sort, rotation, and batch at their defaults (no offset, no queued animation, `OutlineStyle.Full`, `Batches2D.GameplayBatchId`).

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public SpriteComponent(Portrait portrait, int batchId)
```

Creates a sprite that displays a `Portrait` (a fixed sprite + animation-id pair, commonly used for dialogue speaker art) in the given batch.

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \
`batchId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public SpriteComponent(Portrait portrait)
```

Same as the two-argument overload, but renders into the default `Batches2D.GameplayBatchId`.

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \

```csharp
public SpriteComponent(Portrait portrait, int batchId, int yOffset)
```

Same as the `(Portrait, int)` overload, but also sets `YSortOffset` to `yOffset`.

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \
`batchId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`yOffset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public SpriteComponent(Guid guid, Vector2 offset, ImmutableArray<T> id, int ySortOffset, bool rotate, OutlineStyle highlightStyle, int targetSpriteBatch)
```

Full constructor that sets every field explicitly. All of the other constructors ultimately delegate to this one.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`offset` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`id` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`ySortOffset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`rotate` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`highlightStyle` [OutlineStyle](../../Murder/Core/Graphics/OutlineStyle.html) \
`targetSpriteBatch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### AnimationGuid

```csharp
public readonly Guid AnimationGuid { get; init; }
```

The Guid of the Aseprite file ([SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html)) this component renders frames from.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### CurrentAnimation

```csharp
public readonly string CurrentAnimation { get; }
```

Currently playing animation id — simply the first entry of `NextAnimations`, or an empty string if the queue is empty. `SpriteRenderSystem` reads this every frame to select which animation's frame to draw.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### HighlightStyle

```csharp
public readonly OutlineStyle HighlightStyle { get; init; }
```

Outline style drawn around the sprite when it is highlighted (e.g. hovered/selected in the editor, or flagged by gameplay code).

**Returns** \
[OutlineStyle](../../Murder/Core/Graphics/OutlineStyle.html) \

#### NextAnimations

```csharp
public readonly ImmutableArray<T> NextAnimations { get; init; }
```

Ordered queue of animation names to play; the first entry (`CurrentAnimation`) is what's drawn right now, and subsequent entries play in order after each preceding one completes. Use `Play`/`PlayAfter`/`ClearAllNext` to build a new queue rather than mutating this directly, since the component is a `readonly struct`.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Offset

```csharp
public readonly Vector2 Offset;
```

(0,0) is top left and (1,1) is bottom right

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### RotateWithFacing

```csharp
public readonly bool RotateWithFacing { get; init; }
```

When true, the sprite rotates to match the entity's facing angle (read from its `FacingComponent`) instead of staying axis-aligned.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TargetSpriteBatch

```csharp
public readonly int TargetSpriteBatch { get; init; }
```

Sprite batch layer this sprite is rendered into (defaults to `Batches2D.GameplayBatchId`). Marked `[SpriteBatchReference]` so the editor lets you pick from the registered batch ids.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### UseUnscaledTime

```csharp
public readonly bool UseUnscaledTime;
```

When true, animation advances using unscaled (real-world) time, ignoring the game's time-scale — useful for sprites that should keep animating while the game is paused or slowed down.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### YSortOffset

```csharp
public readonly int YSortOffset { get; init; }
```

Pixel offset applied to the entity's Y position when calculating draw order for Y-sorting, letting a tall sprite (e.g. a tree) draw in front of/behind entities near its base without moving the entity itself.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### ClearAllNext()

```csharp
public SpriteComponent ClearAllNext()
```

Returns a new component whose `NextAnimations` contains only `CurrentAnimation`, dropping every queued animation after it. Use this to cancel a queued sequence without interrupting the animation currently playing.

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### HasAnimation(string)

```csharp
public bool HasAnimation(string animationName)
```

Checks whether the `SpriteAsset` referenced by `AnimationGuid` contains an animation with the given name.

**Parameters** \
`animationName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsPlaying(ImmutableArray\<T\>)

```csharp
public bool IsPlaying(ImmutableArray<T> animations)
```

Returns true if the current animation queue exactly matches the provided sequence.

**Parameters** \
`animations` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Play(string[])

```csharp
public SpriteComponent Play(params string[] id)
```

Returns a new component that immediately replaces `NextAnimations` with the given animations, played in order.

**Parameters** \
`id` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### Play(ImmutableArray\<T\>)

```csharp
public SpriteComponent Play(ImmutableArray<T> id)
```

Returns a new component with `NextAnimations` set to `id`, but only if `HasAnimation(id[0])` is true; otherwise the queue is reset to just `CurrentAnimation` (i.e. the request is silently ignored because the target animation doesn't exist on the current sprite asset).

**Parameters** \
`id` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### Play(ImmutableArray\<T\>, Guid?)

```csharp
public SpriteComponent Play(ImmutableArray<T> id, Guid? sprite = null)
```

Like `Play(ImmutableArray<T>)`, but can also switch `AnimationGuid` to a different `sprite` at the same time. The requested animation is accepted if a new `sprite` is supplied, if `id[0]` is the special wildcard `"_"`, or if `HasAnimation(id[0])` is true on the current asset; otherwise the queue falls back to `CurrentAnimation`.

**Parameters** \
`id` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`sprite` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### PlayAfter(IList\<T\>)

```csharp
public SpriteComponent PlayAfter(IList<T> ids)
```

Returns a new component that appends `ids` to the end of `NextAnimations`, queuing them to play after everything already queued finishes, without disturbing the animation currently playing.

**Parameters** \
`ids` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### SetBatch(int)

```csharp
public SpriteComponent SetBatch(int batch)
```

Returns a new component with `TargetSpriteBatch` set to the given batch ID.

**Parameters** \
`batch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### WithBatch(int)

```csharp
public SpriteComponent WithBatch(int batch)
```

Alias for `SetBatch(int)`: returns a new component with `TargetSpriteBatch` set to `batch`. Kept alongside `SetBatch` for the fluent `With...` naming convention used by the rest of the "with"-style methods.

**Parameters** \
`batch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### WithPortrait(Portrait)

```csharp
public SpriteComponent WithPortrait(Portrait portrait)
```

Returns a new component configured to display the given `Portrait`: `AnimationGuid` becomes `portrait.Sprite` and `NextAnimations` becomes `[portrait.AnimationId]`.

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### WithSort(int)

```csharp
public SpriteComponent WithSort(int sort)
```

Returns a new component with `YSortOffset` set to the given value.

**Parameters** \
`sort` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

⚡

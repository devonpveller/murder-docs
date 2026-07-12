# AnimationOverloadComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationOverloadComponent : IComponent
```

Forces an entity's sprite to play a specific animation (or sequence of animations) instead of its default state-machine animation.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Temporarily overrides the sprite animation chosen by an agent's normal locomotion/state logic with a hand-specified clip (or ordered sequence of clips), optionally also swapping the sprite asset itself. Read by `AgentSpriteSystem` (to pick the clip to play instead of idle/walk) and `SpriteRenderSystem` (to know when/what to draw).

**Use-case:** Attach when a cutscene, ability, or scripted action needs to play a one-shot (or multi-step) animation — e.g. an attack windup+swing, an emote, or a death animation — that should override normal movement animations until it finishes, loops out, or is removed. Use `Play(string)` to jump straight to a specific clip, `PlayNext()`/`AtLast` to step through a scripted sequence (`_nextAnimationsOverload`) one clip at a time, and `Now`/`NoLoop`/`FinishCurrentNoLoop` to retime or stop the current clip without rebuilding the whole component.

### ⭐ Constructors

```csharp
public AnimationOverloadComponent()
```

Default (`[JsonConstructor]`) constructor used by the serializer; produces an empty overload with no clips.

```csharp
public AnimationOverloadComponent(ImmutableArray<string> nextAnimationsOverload, Guid customSprite, float start, float duration, bool loop, bool ignoreFacing, ImageFlip flip, int current, float sortOffset, int? supportedDirections, Orientation? orientation)
```

The full constructor: builds an overload from an explicit ordered clip sequence with every playback option specified.

**Parameters** \
`nextAnimationsOverload` [ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`customSprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`flip` [ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \
`current` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`sortOffset` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`supportedDirections` [int?](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`orientation` [Orientation?](../../Murder/Core/Orientation.html) \

```csharp
public AnimationOverloadComponent(ImmutableArray<string> nextAnimationsOverload, Guid customSprite, bool loop, bool ignoreFacing)
```

Creates an overload from an ordered clip sequence, starting immediately (`Start = Game.Now`), with default duration/flip/sort/direction values.

**Parameters** \
`nextAnimationsOverload` [ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`customSprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public AnimationOverloadComponent(string animationId, Guid customSprite, bool loop, bool ignoreFacing)
```

Single-clip convenience constructor with a custom sprite override, starting immediately.

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`customSprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public AnimationOverloadComponent(string animationId, bool loop, bool ignoreFacing)
```

Single-clip convenience constructor, keeping the entity's existing sprite (`customSprite: Guid.Empty`), starting immediately.

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public AnimationOverloadComponent(string animationId, float duration, bool loop, bool ignoreFacing)
```

Single-clip convenience constructor with an explicit maximum `duration`, keeping the entity's existing sprite, starting immediately.

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### Start

```csharp
public readonly float Start { get; public set; }
```

Game time (in seconds, `[JsonIgnore]`d so it is never serialized) at which the overload clip began playing; used together with `Duration` to compute playback progress. Set to `Game.Now` by most convenience constructors and by `Play`/`Now`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Duration

```csharp
public readonly float Duration;
```

Maximum time in seconds to play the current clip before it is considered finished; `-1` (the default) means use the clip's natural length instead of a fixed duration.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Loop

```csharp
public bool Loop { get; public set; }
```

Whether the overload animation should loop continuously (`true`) or play once and stop (`false`, the default).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IgnoreFacing

```csharp
public readonly bool IgnoreFacing { get; public set; }
```

When `true`, the sprite system does not append a directional suffix to the animation name based on the entity's facing — useful for clips that are not authored per-direction (e.g. a full-screen effect or a symmetric emote).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Flip

```csharp
public readonly ImageFlip Flip { get; public set; }
```

Horizontal/vertical flip applied to the clip while this overload is active; defaults to `ImageFlip.None`.

**Returns** \
[ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \

#### Current

```csharp
public readonly int Current { get; public set; }
```

Index into the internal clip sequence identifying which clip is currently playing; advanced by `PlayNext()`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SortOffset

```csharp
public readonly float SortOffset;
```

Extra offset added to the entity's Y-sort draw order while this overload is active.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SupportedDirections

```csharp
public readonly int? SupportedDirections { get; public set; }
```

Optional number of directional variants the overload's clips support (e.g. 4 or 8-way); `null` means unrestricted/not applicable.

**Returns** \
[int?](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SupportedOrientation

```csharp
public readonly Orientation? SupportedOrientation { get; public set; }
```

Optional restriction on which movement orientation(s) this overload's directional clips were authored for; `null` means not restricted.

**Returns** \
[Orientation?](../../Murder/Core/Orientation.html) \

#### CurrentAnimation

```csharp
public string CurrentAnimation { get; }
```

Name of the clip at `Current` in the overload sequence; returns `string.Empty` when the sequence is empty, and logs a warning and returns `string.Empty` if `Current` is out of bounds. Tagged `[ShowInEditor]` so it appears as a read-only field in the inspector.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AnimationCount

```csharp
public readonly int AnimationCount { get; }
```

Total number of clips in the overload sequence.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AtLast

```csharp
public bool AtLast { get; }
```

`true` when `Current` points to the final clip in the sequence, i.e. `PlayNext()` would no longer advance further.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CustomSprite

```csharp
public SpriteAsset CustomSprite { get; }
```

Resolves the sprite asset stored internally (via `[GameAssetId<SpriteAsset>]`) using `Game.Data.TryGetAsset`; `null` if no custom sprite is set or the asset can't be found, in which case the entity's own sprite should be used instead.

**Returns** \
[SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \

#### Now

```csharp
public AnimationOverloadComponent Now { get; }
```

Returns a copy of this component with `Start` reset to `Game.Now`, restarting the current clip's playback timing from the beginning without changing which clip is selected.

**Returns** \
[AnimationOverloadComponent](../../Murder/Components/AnimationOverloadComponent.html) \

#### NoLoop

```csharp
public AnimationOverloadComponent NoLoop { get; }
```

Returns a copy of this component with `Start` reset to `Game.Now` and `Loop` set to `false`, so the clip restarts and then plays exactly once.

**Returns** \
[AnimationOverloadComponent](../../Murder/Components/AnimationOverloadComponent.html) \

#### FinishCurrentNoLoop

```csharp
public AnimationOverloadComponent FinishCurrentNoLoop { get; }
```

Returns a copy of this component collapsed down to a single-clip sequence containing only `CurrentAnimation`, with `Loop` forced to `false` — used to let the currently playing clip finish and stop instead of advancing to further queued clips or looping.

**Returns** \
[AnimationOverloadComponent](../../Murder/Components/AnimationOverloadComponent.html) \

### ⭐ Methods

#### Play(string)

```csharp
public AnimationOverloadComponent Play(string animation)
```

Returns a copy of this component that immediately plays `animation` as a fresh single-clip sequence (`Current` reset to `0`, `Start` reset to `Game.Now`), keeping the rest of the current settings (sprite, duration, loop, flip, sort offset, direction/orientation support).

**Parameters** \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[AnimationOverloadComponent](../../Murder/Components/AnimationOverloadComponent.html) \

#### PlayNext()

```csharp
public AnimationOverloadComponent PlayNext()
```

Advances to the next clip in the sequence (clamped to the last index) and resets `Start` to `Game.Now`, returning the updated component. Combine with `AtLast` to know when the sequence has reached its final clip.

**Returns** \
[AnimationOverloadComponent](../../Murder/Components/AnimationOverloadComponent.html) \

⚡

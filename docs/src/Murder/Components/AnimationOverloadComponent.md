# AnimationOverloadComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationOverloadComponent : IComponent
```

Forces an entity's sprite to play a specific animation (or sequence of animations) instead of its default state-machine animation.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Temporarily overrides the sprite animation chosen by the agent or state-machine system with a hand-specified clip.

**Use-case:** Attach when a cutscene or ability needs to play a one-shot animation clip (e.g., an attack or emote) that should override normal locomotion animations until it finishes or is removed.

### ⭐ Constructors
```csharp
public AnimationOverloadComponent()
```

```csharp
public AnimationOverloadComponent(ImmutableArray<T> animationId, Guid customSprite, float start, bool loop, bool ignoreFacing)
```

**Parameters** \
`animationId` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`customSprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public AnimationOverloadComponent(ImmutableArray<T> animations, float duration, bool loop, bool ignoreFacing, int current, float sortOffset, Guid customSprite, float start)
```

**Parameters** \
`animations` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`current` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`sortOffset` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`customSprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public AnimationOverloadComponent(ImmutableArray<T> animations, float duration, bool loop, bool ignoreFacing, int current, float sortOffset, Guid customSprite)
```

**Parameters** \
`animations` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`current` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`sortOffset` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`customSprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public AnimationOverloadComponent(string animationId, bool loop, bool ignoreFacing, float startTime)
```

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public AnimationOverloadComponent(string animationId, bool loop, bool ignoreFacing)
```

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public AnimationOverloadComponent(string animationId, float duration, bool loop, bool ignoreFacing, float startTime)
```

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public AnimationOverloadComponent(string animationId, float duration, bool loop, bool ignoreFacing, int current, float sortOffset, Guid customSprite)
```

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`current` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`sortOffset` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`customSprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public AnimationOverloadComponent(string animationId, float duration, bool loop, bool ignoreFacing)
```

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public AnimationOverloadComponent(string animationId, Guid customSprite, float start, bool loop, bool ignoreFacing)
```

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`customSprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`loop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`ignoreFacing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### AnimationCount
```csharp
public int AnimationCount { get; }
```

Total number of animation clips in the overload sequence.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### AnimationId
```csharp
public string AnimationId { get; }
```

Name of the first animation clip in the overload sequence (legacy single-clip accessor).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### AtLast
```csharp
public bool AtLast { get; }
```

`true` when `Current` points to the final clip in the sequence.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Current
```csharp
public readonly int Current;
```

Index of the clip currently playing within the animation sequence.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### CurrentAnimation
```csharp
public string CurrentAnimation { get; }
```

Name of the animation clip at `Current` index; returns an empty string when the sequence is empty.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### CustomSprite
```csharp
public SpriteAsset CustomSprite { get; }
```

Optional sprite asset that replaces the entity's default sprite while this overload is active; `null` if no replacement is set.

**Returns** \
[SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
#### Duration
```csharp
public readonly float Duration;
```

Maximum time in seconds to play the animation; `-1` means use the clip's natural length.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### IgnoreFacing
```csharp
public readonly bool IgnoreFacing;
```

When `true`, the sprite system will not append directional suffixes to the animation name based on the entity's facing direction.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Loop
```csharp
public readonly bool Loop;
```

Whether the overload animation should loop continuously or play once and stop.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### NoLoop
```csharp
public AnimationOverloadComponent NoLoop { get; }
```

Returns a copy of this component with `Loop` set to `false`.

**Returns** \
[AnimationOverloadComponent](../../Murder/Components/AnimationOverloadComponent.html) \
#### Now
```csharp
public AnimationOverloadComponent Now { get; }
```

Returns a copy of this component with `Start` set to the current game time, causing the animation to begin immediately.

**Returns** \
[AnimationOverloadComponent](../../Murder/Components/AnimationOverloadComponent.html) \
#### SortOffset
```csharp
public readonly float SortOffset;
```

Vertical offset added to the entity's Y position when computing draw-order sorting while this overload is active.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Start
```csharp
public readonly float Start;
```

Game time (in seconds) at which the overload animation began playing, used to compute the current playback position.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### PlayNext()
```csharp
public AnimationOverloadComponent PlayNext()
```

Advances to the next clip in the sequence, returning a new component with `Current` incremented.

**Returns** \
[AnimationOverloadComponent](../../Murder/Components/AnimationOverloadComponent.html) \



⚡
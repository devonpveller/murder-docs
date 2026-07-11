# SpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteComponent : IComponent
```

Primary rendering component for Aseprite-based sprites. Stores the animation asset reference, current animation queue, render offset, Y-sort value, and related display options.

**Intent:** Drive sprite rendering and animation playback for any entity that displays an Aseprite sprite.

**Use-case:** Attach to any game-world entity that should render a sprite; set `AnimationGuid` to the target `SpriteAsset`, populate `NextAnimations` with the desired animation sequence, and let the rendering system handle the rest.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public SpriteComponent()
```

```csharp
public SpriteComponent(Portrait portrait, int batchId)
```

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \
`batchId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public SpriteComponent(Portrait portrait)
```

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \

```csharp
public SpriteComponent(Guid guid, Vector2 offset, ImmutableArray<T> id, int ySortOffset, bool rotate, bool flip, OutlineStyle highlightStyle, int targetSpriteBatch)
```

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`offset` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`id` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`ySortOffset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`rotate` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`flip` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`highlightStyle` [OutlineStyle](../../Murder/Core/Graphics/OutlineStyle.html) \
`targetSpriteBatch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### AnimationGuid
```csharp
public Guid AnimationGuid { get; public set; }
```

The Guid of the Aseprite file.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### CurrentAnimation
```csharp
public string CurrentAnimation { get; }
```

Current playing animation id.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FlipWithFacing
```csharp
public readonly bool FlipWithFacing;
```

When true, the sprite is horizontally flipped to match the entity's facing direction.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### HighlightStyle
```csharp
public OutlineStyle HighlightStyle { get; public set; }
```

Outline style drawn around the sprite when it is highlighted.

**Returns** \
[OutlineStyle](../../Murder/Core/Graphics/OutlineStyle.html) \
#### NextAnimations
```csharp
public ImmutableArray<T> NextAnimations { get; public set; }
```

Ordered queue of animation names to play; the first entry is the current animation, subsequent entries play after it completes.

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
public readonly bool RotateWithFacing;
```

When true, the sprite rotates to match the entity's facing angle instead of flipping.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### TargetSpriteBatch
```csharp
public readonly int TargetSpriteBatch;
```

Sprite batch layer this sprite is rendered into.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### UseUnscaledTime
```csharp
public readonly bool UseUnscaledTime;
```

When true, animation advances using unscaled (real-world) time, ignoring game time-scale.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### YSortOffset
```csharp
public int YSortOffset { get; public set; }
```

Pixel offset applied to the entity's Y position when calculating draw order for Y-sorting.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### HasAnimation(string)
```csharp
public bool HasAnimation(string animationName)
```

Checks whether the referenced sprite asset contains an animation with the given name.

**Parameters** \
`animationName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsPlaying(ImmutableArray<T>)
```csharp
public bool IsPlaying(ImmutableArray<T> animations)
```

Returns true if the current animation queue exactly matches the provided sequence.

**Parameters** \
`animations` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Play(ImmutableArray<T>)
```csharp
public SpriteComponent Play(ImmutableArray<T> id)
```

Returns a new component with `NextAnimations` set to the provided animation list.

**Parameters** \
`id` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### Play(String[])
```csharp
public SpriteComponent Play(String[] id)
```

Returns a new component playing the specified animations in sequence.

**Parameters** \
`id` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### PlayAfter(string)
```csharp
public SpriteComponent PlayAfter(string id)
```

Returns a new component that queues the specified animation to play after the current one finishes.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

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

#### WithPortrait(Portrait)
```csharp
public SpriteComponent WithPortrait(Portrait portrait)
```

Returns a new component configured to display the given portrait.

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
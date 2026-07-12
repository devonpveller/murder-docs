# QuickSpriteInfo

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct QuickSpriteInfo
```

A lightweight, all-in-one description of a sprite to play once and forget: which `SpriteAsset` to use, which animation(s) to play in sequence, and how to position/tint/sort it.

**Intent:** Intended for one-shot VFX (hit sparks, pickup pop, screen-space UI blips) that are spawned procedurally rather than authored as a full entity/component graph, avoiding the boilerplate of assembling a sprite + animation component pair by hand for a throwaway effect. Struct for creating one-shot animations and other similar sprite effects.

**Use-case:** Build a `QuickSpriteInfo` describing the sprite/animation/tint you want, then hand it to whatever helper spawns transient VFX entities in your game/services layer. Use the `Portrait` constructor to reuse a dialogue portrait's sprite/animation as a quick effect.

### ⭐ Constructors

```csharp
public QuickSpriteInfo(Guid sprite)
```

Creates a quick sprite for `sprite` with no animation set yet (populate `Animations` separately via a `with` expression).

**Parameters** \
`sprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public QuickSpriteInfo(Portrait portrait)
```

Creates a quick sprite that plays the single animation referenced by a dialogue `Portrait`.

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \

### ⭐ Properties

#### Animations

```csharp
public readonly ImmutableArray<string> Animations { get; public set; }
```

Names of the animation(s) within `Sprite` to play, in order.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Flip

```csharp
public readonly ImageFlip Flip { get; public set; }
```

Horizontal/vertical mirroring applied when drawing the sprite.

**Returns** \
[ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \

#### Offset

```csharp
public readonly Vector2 Offset { get; public set; }
```

Pixel offset applied to the sprite's draw position.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Sprite

```csharp
public readonly Guid Sprite { get; public set; }
```

GUID of the `SpriteAsset` (aseprite) to draw.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### TargetSpriteBatch

```csharp
public readonly int TargetSpriteBatch { get; public set; }
```

Which sprite batch (see `Batches2D`) the sprite is drawn into. Defaults to `Batches2D.GameplayBatchId`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Tint

```csharp
public readonly Color Tint { get; public set; }
```

Color tint multiplied into the sprite when drawing. Defaults to no tint (white).

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### YSortOffset

```csharp
public readonly int YSortOffset { get; public set; }
```

Extra offset added to the sprite's Y-sort value, used to nudge draw order relative to other sprites at the same position.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

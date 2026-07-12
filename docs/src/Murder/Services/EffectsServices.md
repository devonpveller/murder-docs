# EffectsServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class EffectsServices
```

Helpers for spawning one-shot visual effects, screen transitions, and highlight/solidity toggles in the game world.

**Intent:** Provides high-level methods for common visual effects — quick throwaway sprites, fade-in/fade-out screen transitions, entity highlighting, and one-shot animations — so callers don't need to hand-assemble the component combinations each effect requires.

**Use-case:** Call `CreateQuickSprite` to spawn a short-lived visual (impact flash, particle-like sprite) parented to another entity. Call `FadeIn`/`FadeOut` to create screen transitions between scenes or during pause/loading. Call `ApplyHighlight`/`RemoveHighlight` to visually mark an entity (and correctly propagate the highlight to children when the entity uses `HighlightOnChildrenComponent`). Call `PlayAnimationAt` to spawn a one-shot sprite animation at a world position (e.g. an explosion). Call `RemoveSolid` to strip the `SOLID` collision flag from an entity or its `"solid"` child, e.g. when a wall or door becomes passable.

### ⭐ Methods

#### CreateQuickSprite(World, QuickSpriteInfo, Entity, bool)

```csharp
public static Entity CreateQuickSprite(World world, QuickSpriteInfo info, Entity? parent = null, bool destroyAfter = true)
```

Spawns a new entity configured from `info` (sprite, animation, offset, flip, tint, sort/batch) with `SpriteComponent`, `PositionComponent`, `FlipSpriteComponent`, `TintComponent`, and a `DoNotPersistEntityOnSaveComponent` so it's never written into save data. When `destroyAfter` is `true` (the default) the entity is set to self-destroy once its animation finishes, making this ideal for one-shot VFX. If `parent` is provided, the new entity is added as its child under a generated name (`quick_sprite_N`), so it moves and is destroyed together with the parent.

**Parameters** \
`world` [World](../../Bang/World.html) \
`info` [QuickSpriteInfo](../../Murder/Core/QuickSpriteInfo.html) \
`parent` [Entity](../../Bang/Entities/Entity.html) \
`destroyAfter` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### FadeIn(World, float, Color, float, int, string)

```csharp
public static Entity? FadeIn(World world, float time, Color color, float sorting = 0, int? targetBatch = null, string? customTexture = null)
```

Adds an entity carrying a `FadeScreenComponent` that darkens the screen to `color` over `time` seconds. Returns `null` (spawning nothing) while `Game.Instance.IsSkippingDeltaTimeOnUpdate` is `true`, to avoid creating a fade during frames where delta time is being skipped (e.g. very first frame / resize). `customTexture`, when provided (or when a `CustomFadeScreenStyleComponent` is set on the world), is resolved to an `images/`-relative path and used instead of a flat color fade.

**Parameters** \
`world` [World](../../Bang/World.html) \
`time` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`targetBatch` [int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`customTexture` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### FadeOut(World, float, Color, float, int)

```csharp
public static void FadeOut(World world, float duration, Color color, float delay = 0, int bufferDrawFrames = 0)
```

Destroys any existing `FadeScreenComponent` entities and adds a new one that fades the screen to `color` (clearing it) over `duration` seconds, after an optional `delay`. Does nothing while `Game.Instance.IsSkippingDeltaTimeOnUpdate` is `true`. When `bufferDrawFrames` is greater than zero, the fade start time is scheduled relative to `delay` alone (rather than `Game.NowUnscaled + delay`) to avoid glitches at low frame rates where the buffered frames need to render before the timer starts.

**Parameters** \
`world` [World](../../Bang/World.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`delay` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bufferDrawFrames` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ApplyHighlight(World, Entity, HighlightSpriteComponent)

```csharp
public static void ApplyHighlight(World world, Entity e, HighlightSpriteComponent highlight)
```

Applies `highlight` to `e`. If `e` has a `HighlightOnChildrenComponent`, the highlight is instead routed to a named child (if `Child` is set) or to every child of `e`'s root entity, so composite entities (e.g. a multi-part prop) highlight consistently. If `e` itself has no sprite, the highlight is applied to its root entity instead, so highlighting a sub-part still visually marks the whole object.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`highlight` [HighlightSpriteComponent](../../Murder/Components/HighlightSpriteComponent.html) \

#### RemoveHighlight(Entity)

```csharp
public static void RemoveHighlight(Entity e)
```

Removes the highlight effect applied by `ApplyHighlight`, mirroring the same child/root-entity routing logic so the highlight is cleared from wherever it was actually applied.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### PlayAnimationAt(World, Portrait, Vector2)

```csharp
public static void PlayAnimationAt(World world, Portrait blastAnimation, Vector2 position)
```

Spawns a new entity at `position` with a `SpriteComponent` built from `blastAnimation` and a `DestroyOnAnimationCompleteComponent`, so the animation plays once and the entity is automatically cleaned up. Typical use is a one-shot visual like an impact/explosion/blast effect.

**Parameters** \
`world` [World](../../Bang/World.html) \
`blastAnimation` [Portrait](../../Murder/Core/Portrait.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### RemoveSolid(Entity)

```csharp
public static void RemoveSolid(Entity e)
```

Clears the `SOLID` bit from the `Layer` of `e`'s collider — checking `e` itself first, and falling back to a child named `"solid"` if `e` has no collider of its own. Does nothing if neither `e` nor a `"solid"` child has a collider, or if the collider isn't currently flagged `SOLID`. Use this to make a wall, door, or obstacle passable at runtime while keeping any other collision layers (e.g. trigger/hole detection) intact.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

⚡

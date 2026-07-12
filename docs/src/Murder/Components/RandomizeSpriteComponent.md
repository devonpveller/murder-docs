# RandomizeSpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RandomizeSpriteComponent : IComponent
```

Applies random cosmetic variation to a sprite when it is (re)activated: can randomise which animation plays, where it starts within that animation, and whether the sprite is rotated or flipped.

**Intent:** Introduce cheap visual variety among many identical sprite entities without needing separate assets.

**Use-case:** Attach to entities spawned in bulk (props, foliage, tile decorations) so identical prefab instances do not all look and animate in lockstep. `RandomizeAsepriteSystem` watches for this component alongside [SpriteComponent](../../Murder/Components/SpriteComponent.html) and re-rolls the requested variations every time the component is added or the entity is re-activated.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Properties

#### RandomizeAnimation

```csharp
public readonly bool RandomizeAnimation;
```

When true, a random animation is picked out of the sprite asset's animation set (the empty/default animation is excluded) and set as the entity's active animation.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RandomizeAnimationStart

```csharp
public readonly bool RandomizeAnimationStart;
```

When true, the animation is started at a random point (between 1 and 32 frames of elapsed time) instead of frame zero, so multiple copies of the same animation are visually out of phase.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RandomRotate

```csharp
public readonly bool RandomRotate;
```

When true, the entity is given a random cardinal facing direction and its sprite is set to rotate to match that facing, in 90 degree increments.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RandomFlip

```csharp
public readonly bool RandomFlip;
```

When true, there is a 50% chance the sprite is horizontally flipped, mirroring the artwork.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡

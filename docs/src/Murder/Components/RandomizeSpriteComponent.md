# RandomizeSpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RandomizeSpriteComponent : IComponent
```

Applies random visual variation to a sprite when the entity is created: can randomise which animation plays, where it starts within that animation, and whether the sprite is rotated or flipped.

**Intent:** Introduce cheap visual variety among many identical sprite entities without needing separate assets.

**Use-case:** Attach to tile entities, props, or particle-like entities so each instance appears slightly different from its neighbours.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Properties
#### RandomizeAnimation
```csharp
public readonly bool RandomizeAnimation;
```

When true, a random animation from the sprite asset is selected on spawn.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### RandomizeAnimationStart
```csharp
public readonly bool RandomizeAnimationStart;
```

When true, the animation starts at a random frame rather than frame zero.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### RandomRotate
```csharp
public readonly bool RandomRotate;
```

When true, the sprite is rotated by a random multiple of 90 degrees on spawn.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \


⚡
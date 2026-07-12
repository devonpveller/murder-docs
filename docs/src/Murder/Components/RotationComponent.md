# RotationComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RotationComponent : IComponent
```

Adds a free rotation angle to an entity's rendering, independent of the entity's facing/movement direction.

**Intent:** Track a free-rotation angle that is applied on top of any facing-derived rotation when the sprite is drawn.

**Use-case:** Attach to projectiles, particles, or objects that spin freely and have nothing to do with gameplay direction — e.g. a rotating coin pickup, a spinning saw blade, or debris tumbling in the air. `SpriteRenderSystem` (and the equivalent editor debug renderer) read this component and add `Rotation` on top of any facing-derived rotation before drawing the sprite.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public RotationComponent()
```

Creates a component with no rotation (0 radians).

```csharp
public RotationComponent(float rotation)
```

Creates a component with the given rotation.

**Parameters** \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Rotation

```csharp
public readonly float Rotation;
```

Rotation angle applied to the entity's sprite when rendering, in radians.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

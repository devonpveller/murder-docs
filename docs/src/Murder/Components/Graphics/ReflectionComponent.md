# ReflectionComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct ReflectionComponent : IComponent
```

Configures a water/mirror reflection rendering pass for the entity's sprite.

**Intent:** Instruct the render system to draw a flipped, semi-transparent copy of the entity's sprite below it to simulate a reflective surface.

**Use-case:** Add to characters or objects that should appear reflected in water or a mirror; adjust `Alpha` for reflection opacity, `Offset` to shift the reflected image, and set `BlockReflection` to hide the reflection entirely.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public ReflectionComponent()
```

### ⭐ Properties
#### Alpha
```csharp
public readonly float Alpha;
```

Opacity of the reflection image, where 0 is fully transparent and 1 is fully opaque.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### BlockReflection
```csharp
public readonly bool BlockReflection;
```

When `true`, suppresses rendering of the reflection for this entity even if a reflection layer is present.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Offset
```csharp
public readonly Vector2 Offset;
```

Pixel offset applied to the reflected image's position relative to the original sprite.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \


⚡
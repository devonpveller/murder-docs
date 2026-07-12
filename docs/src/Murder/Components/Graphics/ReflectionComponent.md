# ReflectionComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct ReflectionComponent : IComponent
```

Configures a vertically-flipped, semi-transparent "mirror" copy of the entity's sprite, drawn to simulate a reflective floor surface.

**Intent:** Let level/scene authors mark which entities should show a reflection without hardcoding it into a render system. Note that reading this component is currently only implemented by the **editor's** debug/preview renderer (`Murder.Editor.Systems.SpriteRenderDebugSystem`, an `[EditorSystem]`), which checks the stage's "show reflections" toggle and, when a `ReflectionComponent` is present and `BlockReflection` is `false`, draws the sprite flipped on the Y axis (`Scale * (1, -1)`) into the floor batch with `Color = spriteColor * Alpha`. The gameplay `SpriteRenderSystem` used at runtime does not currently read this component, so today this is effectively an in-editor visualization aid rather than a shipped rendering feature — keep that in mind before relying on it for a released build's visuals.

**Use-case:** Add to characters or objects that should preview as reflected in water or a mirror while working in the level editor; adjust `Alpha` for reflection opacity, `Offset` to shift the reflected image relative to the source sprite, and set `BlockReflection` to `true` to temporarily hide the reflection without removing the component.

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

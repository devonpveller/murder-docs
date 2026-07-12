# AlphaComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AlphaComponent : IComponent
```

Set alpha of a component being displayed in the screen.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a single, simple opacity value for an entity's rendering, independent of that entity's other components (e.g. `SpriteRendererComponent`'s own tint). This lets systems fade an entity in or out without needing to know about or overwrite its rendering-specific state.

**Use-case:** Attach to any renderable entity and read `Alpha` from render systems / draw-info construction to scale the sprite's transparency — for example a fade-in/fade-out effect, a "recently seen" dimming effect, or any system that needs to temporarily make an entity translucent. Multiple systems writing to this component will overwrite each other's value, since there is only a single `Alpha` slot (there is no per-source blending); coordinate ownership of this component if more than one system needs to drive an entity's fade.

### ⭐ Constructors

```csharp
public AlphaComponent()
```

Creates a component with `Alpha` at its default of `1f` (fully opaque).

```csharp
public AlphaComponent(float amount)
```

Creates a component with `Alpha` set to `amount`.

**Parameters** \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Alpha

```csharp
public readonly float Alpha;
```

The opacity value for this entity's rendering, from `0` (fully transparent) to `1` (fully opaque, the default). Values outside that range are not clamped by the component itself.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

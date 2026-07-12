# GlobalShaderComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct GlobalShaderComponent : IComponent
```

Holds parameters for the global post-processing shader applied to the entire render output.

**Intent:** Provide a single source of truth for screen-wide shader effects (currently dithering) that the render pipeline can read from, instead of hardcoding the value or duplicating it per-entity.

**Use-case:** Attach to the world or camera entity once and adjust `DitherAmount` to control the global dither intensity intended for the rendering pipeline's dithering shader.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public GlobalShaderComponent()
```

Creates a global shader component with the default dither amount.

### ⭐ Properties

#### DitherAmount

```csharp
public readonly float DitherAmount;
```

Strength of the global dither effect, from 0 (no dithering) to 1 (maximum dithering), intended for the dithering shader used by the render pipeline to reduce color banding.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡

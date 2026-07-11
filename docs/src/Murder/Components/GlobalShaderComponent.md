# GlobalShaderComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct GlobalShaderComponent : IComponent
```

Holds parameters for a shader effect that is applied globally to the entire render context, affecting all rendered output.

**Intent:** Configure world-wide post-processing shader settings (such as dithering) from a single entity.

**Use-case:** Attach to the world or camera entity once and adjust `DitherAmount` to control the global dither intensity passed to the rendering pipeline.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public GlobalShaderComponent()
```

### ⭐ Properties
#### DitherAmount
```csharp
public readonly float DitherAmount;
```

Intensity of the global dither effect applied to the render output, ranging from 0 (no dither) to 1 (full dither).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡
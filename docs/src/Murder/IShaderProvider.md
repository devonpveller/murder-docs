# IShaderProvider

**Namespace:** Murder \
**Assembly:** Murder.dll

```csharp
public abstract IShaderProvider
```

A game that leverages murder and use custom shaders should implement this in their [IMurderGame](../Murder/IMurderGame.html).

**Intent:** Declares the contract for a game that supplies custom GPU shaders to the Murder rendering pipeline. Implement this interface alongside `IMurderGame` to inject additional GLSL/HLSL shader files that are loaded at startup.

**Use-case:** When your game needs post-processing effects, custom sprite shaders, or any non-default rendering pass, implement `IShaderProvider` on your `IMurderGame` class and return the shader filenames from `Shaders`. The engine resolves those names against the `resources/` folder and compiles them into the render pipeline.

### ⭐ Properties
#### Shaders
```csharp
public abstract virtual String[] Shaders { get; }
```

Names of custom shaders that will be provided. Each name maps to a compiled shader file placed at `<game_directory>/../resources`. The engine iterates this array at startup to load and register every custom shader effect.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡
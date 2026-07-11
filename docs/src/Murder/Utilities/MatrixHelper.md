# MatrixHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class MatrixHelper
```

Conversion helpers between `System.Numerics.Matrix4x4` and the MonoGame/XNA `Matrix` type.

**Intent:** Bridges the gap between the engine's use of `System.Numerics` math types and MonoGame's XNA matrix type.

**Use-case:** Call `ToXnaMatrix` when passing a System.Numerics matrix to MonoGame rendering APIs that require an XNA `Matrix`.

### ⭐ Methods
#### ToXnaMatrix(Matrix4x4)
```csharp
public Matrix ToXnaMatrix(Matrix4x4 matrix)
```

Converts a `System.Numerics.Matrix4x4` to a MonoGame `Matrix`.

**Parameters** \
`matrix` [Matrix4x4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Matrix4x4?view=net-7.0) \

**Returns** \
[Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \



⚡
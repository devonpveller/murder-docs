# ShaderHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class ShaderHelper
```

Extension methods for setting typed parameters on MonoGame `Effect` objects by their shader variable name.

**Intent:** Provides a type-safe, overload-based API for applying shader parameters, eliminating direct calls to `Effect.Parameters[name].SetValue`.

**Use-case:** Call `SetParameter` on any loaded effect to apply textures, vectors, colors, or scalars by their shader variable name.

### ⭐ Methods
#### SetParameter(Effect, string, Texture2D)
```csharp
public void SetParameter(Effect effect, string id, Texture2D val)
```

Sets the `Texture2D` shader parameter named `id` on the given effect.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html)

#### SetParameter(Effect, string, Vector2)
```csharp
public void SetParameter(Effect effect, string id, Vector2 val)
```

Sets the `Vector2` (XNA) shader parameter named `id` on the given effect.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

#### SetParameter(Effect, string, Vector3)
```csharp
public void SetParameter(Effect effect, string id, Vector3 val)
```

Sets the `Vector3` shader parameter named `id` on the given effect.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### SetParameter(Effect, string, Vector3[])
```csharp
public void SetParameter(Effect effect, string id, Vector3[] val)
```

Sets the `Vector3` array shader parameter named `id` on the given effect.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector3[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### SetParameter(Effect, string, Point)
```csharp
public void SetParameter(Effect effect, string id, Point val)
```

Sets the `Point` shader parameter named `id` on the given effect as a two-component integer vector.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Point](../../Murder/Core/Geometry/Point.html) \

#### SetParameter(Effect, string, bool)
```csharp
public void SetParameter(Effect effect, string id, bool val)
```

Sets the `bool` shader parameter named `id` on the given effect.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetParameter(Effect, string, float)
```csharp
public void SetParameter(Effect effect, string id, float val)
```

Sets the `float` scalar shader parameter named `id` on the given effect.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetParameter(Effect, string, int)
```csharp
public void SetParameter(Effect effect, string id, int val)
```

Sets the `int` scalar shader parameter named `id` on the given effect.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetParameter(Effect, string, Vector2)
```csharp
public void SetParameter(Effect effect, string id, Vector2 val)
```

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SetTechnique(Effect, string)
```csharp
public void SetTechnique(Effect effect, string id)
```

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TrySetParameter(Effect, string, Vector2)
```csharp
public void TrySetParameter(Effect effect, string id, Vector2 val)
```

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

#### TrySetParameter(Effect, string, bool)
```csharp
public void TrySetParameter(Effect effect, string id, bool val)
```

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TrySetParameter(Effect, string, float)
```csharp
public void TrySetParameter(Effect effect, string id, float val)
```

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TrySetParameter(Effect, string, int)
```csharp
public void TrySetParameter(Effect effect, string id, int val)
```

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
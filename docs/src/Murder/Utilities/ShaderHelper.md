# ShaderHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class ShaderHelper
```

Extension methods for reading and writing named parameters/techniques on MonoGame `Effect` instances, wrapping the raw `effect.Parameters[name]` indexer access with null-checks and logging.

**Intent:** Two families are provided: `SetParameter`, which logs a warning (or catches and logs a set failure) when the parameter doesn't exist or can't accept the value — use this for parameters the shader is expected to declare; and `TrySetParameter`, which silently no-ops when the parameter is missing — use this for optional parameters that not every shader variant defines.

**Use-case:** Call `SetParameter`/`TrySetParameter` on any loaded effect to apply textures, vectors, colors, or scalars by their shader variable name; call `SetTechnique` to switch which technique the effect uses before drawing.

### ⭐ Methods

#### SetTechnique(Effect, string)

```csharp
public void SetTechnique(Effect effect, string id)
```

Switches the effect's active technique to the one named `id`. Logs an error (instead of throwing) if no technique with that name exists on the effect, so a missing/renamed technique degrades gracefully instead of crashing the render loop.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TrySetParameter(Effect, string, bool)

```csharp
public void TrySetParameter(Effect effect, string id, bool val)
```

Sets a `bool` shader parameter if it exists on the effect; silently does nothing otherwise.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetParameter(Effect, string, bool)

```csharp
public void SetParameter(Effect effect, string id, bool val)
```

Sets a `bool` shader parameter, logging a warning if the effect has no parameter named `id`.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TrySetParameter(Effect, string, int)

```csharp
public void TrySetParameter(Effect effect, string id, int val)
```

Sets an `int` shader parameter if it exists on the effect; silently does nothing otherwise.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetParameter(Effect, string, int)

```csharp
public void SetParameter(Effect effect, string id, int val)
```

Sets an `int` shader parameter, logging a warning if the effect has no parameter named `id`.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### TrySetParameter(Effect, string, float)

```csharp
public void TrySetParameter(Effect effect, string id, float val)
```

Sets a `float` shader parameter if it exists on the effect; silently does nothing otherwise.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TrySetParameter(Effect, string, Vector2)

```csharp
public void TrySetParameter(Effect effect, string id, Vector2 val)
```

Sets an XNA `Vector2` shader parameter if it exists on the effect; silently does nothing otherwise.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

#### SetParameter(Effect, string, float)

```csharp
public void SetParameter(Effect effect, string id, float val)
```

Sets a `float` shader parameter, logging a warning if the effect has no parameter named `id`.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetParameter(Effect, string, Vector3[])

```csharp
public void SetParameter(Effect effect, string id, Vector3[] val)
```

Sets an XNA `Vector3` array shader parameter, logging a warning if the effect has no parameter named `id`.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector3[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### SetParameter(Effect, string, Point)

```csharp
public void SetParameter(Effect effect, string id, Point val)
```

Sets a shader parameter from an engine `Point` by converting it to an XNA `Vector2` first.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Point](../../Murder/Core/Geometry/Point.html) \

#### SetParameter(Effect, string, Vector2)

```csharp
public void SetParameter(Effect effect, string id, Vector2 val)
```

Sets a shader parameter from a `System.Numerics.Vector2` by converting it to an XNA `Vector2` first.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SetParameter(Effect, string, Vector3)

```csharp
public void SetParameter(Effect effect, string id, Vector3 val)
```

Sets an XNA `Vector3` shader parameter, logging an error if the value can't be applied and a warning if the parameter doesn't exist.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### SetParameter(Effect, string, Vector2)

```csharp
public void SetParameter(Effect effect, string id, Vector2 val)
```

Sets an XNA `Vector2` shader parameter directly, logging an error if the value can't be applied and a warning if the parameter doesn't exist.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

#### SetParameter(Effect, string, Texture2D)

```csharp
public void SetParameter(Effect effect, string id, Texture2D val)
```

Binds a `Texture2D` to a shader's texture sampler parameter, logging a warning if the effect has no parameter named `id`.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### SetParameter(Effect, string, Texture3D)

```csharp
public void SetParameter(Effect effect, string id, Texture3D val)
```

Binds a `Texture3D` (e.g. a 3D LUT) to a shader parameter, logging a warning if the effect has no parameter named `id`.

**Parameters** \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`val` [Texture3D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture3D.html) \

#### TryGetAnotationVector2(EffectParameter, string)

```csharp
public Vector2? TryGetAnotationVector2(EffectParameter parameter, string anotationName)
```

Reads a shader parameter's declared annotation (from the `.fx` source, e.g. `<defaultValue = ...>`) as a `Vector2`. Returns `null` and logs an error if the annotation is missing, is not a vector, or fails to parse. Used to read author-specified default/metadata values embedded in shader files.

**Parameters** \
`parameter` [EffectParameter](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.EffectParameter.html) \
`anotationName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0)? \

⚡

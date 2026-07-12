# MurderBlendState

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum MurderBlendState : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

The GPU blend state used when compositing a batch's sprites onto the render target.

**Intent:** Selects the MonoGame `BlendState` a `Batch2D` should switch to for a given sprite (alpha blend vs. additive), translated internally by `Batch2D.SetBlendState`. This is distinct from `BlendStyle`, which controls the shader-level color math rather than the GPU compositing mode.

**Use-case:** Set `DrawInfo.BlendState` to `Additive` for glow, light, and particle sprites that should brighten the background instead of occluding it; leave it at the default `AlphaBlend` for ordinary sprites.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Additive

```csharp
public static const MurderBlendState Additive;
```

Additive blending, where the sprite's color is added to the framebuffer rather than replacing it. Useful for glow, light, and particle effects that should brighten whatever is beneath them.

**Returns** \
[MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \

#### AlphaBlend

```csharp
public static const MurderBlendState AlphaBlend;
```

Standard alpha blending, where the sprite's color is composited over the framebuffer according to its alpha. This is the default for virtually all sprite rendering.

**Returns** \
[MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \

⚡

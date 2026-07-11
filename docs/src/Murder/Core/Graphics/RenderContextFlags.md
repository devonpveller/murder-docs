# RenderContextFlags

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum RenderContextFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

These are the flags consumed by [RenderContext](../../../Murder/Core/Graphics/RenderContext.html).

**Intent:** Provides a bitmask to opt in to optional `RenderContext` features such as debug draw batches and custom shader post-processing.

**Use-case:** Pass the appropriate flags when overriding `Game.CreateRenderContext()` to enable the capabilities your render pipeline needs.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### CustomShaders
```csharp
public static const RenderContextFlags CustomShaders;
```

Whether it should apply custom shaders as part of the processing.

**Returns** \
[RenderContextFlags](../../../Murder/Core/Graphics/RenderContextFlags.html) \
#### Debug
```csharp
public static const RenderContextFlags Debug;
```

Whether it should set the debug batches.

**Returns** \
[RenderContextFlags](../../../Murder/Core/Graphics/RenderContextFlags.html) \
#### None
```csharp
public static const RenderContextFlags None;
```

No optional rendering features are enabled.

**Returns** \
[RenderContextFlags](../../../Murder/Core/Graphics/RenderContextFlags.html) \


⚡
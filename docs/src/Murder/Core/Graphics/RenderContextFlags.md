# RenderContextFlags

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum RenderContextFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

These are the flags consumed by [RenderContext](../../../Murder/Core/Graphics/RenderContext.html).

**Intent:** Provides a bitmask to opt in to optional `RenderContext` features such as debug draw batches and custom shader post-processing.

**Use-case:** Pass the appropriate flags when overriding `Game.CreateRenderContext()` to enable the capabilities your render pipeline needs. `RenderContext`'s constructor stores this bitmask on its `Settings` field and reads it at a few key points: `Debug` decides (in `Initialize`) whether the debug sprite batches and debug render target get allocated at all, and `Editor` forces `RefreshWindow` to use `ScalingKind.ThreeX` regardless of the player's scaling preference (used when the render context is hosted inside the editor's viewport panel rather than a real game window).

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

Whether it should set the debug batches. When set, `RenderContext` allocates `DebugBatch`/`DebugFxBatch` and a dedicated debug render target, and composites them on top of the final frame in `End()`; when unset, those batches don't exist and `DebugBatch`/`DebugFxBatch` must not be used.

**Returns** \
[RenderContextFlags](../../../Murder/Core/Graphics/RenderContextFlags.html) \

#### Editor

```csharp
public static const RenderContextFlags Editor;
```

Whether it should set the editor batches. In practice this flag forces the render context's viewport scaling to `ScalingKind.ThreeX` instead of the user's normal scaling preference, since the editor hosts the game view inside a resizable panel rather than the actual game window.

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

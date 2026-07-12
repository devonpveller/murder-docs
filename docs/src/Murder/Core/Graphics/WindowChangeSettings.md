# WindowChangeSettings

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct WindowChangeSettings
```

Describes a pending change to the game window/viewport.

**Intent:** Carries the requested size, native (design) resolution, scaling mode, and a force flag from a window-resize or preference-change event through to the next frame, where `RenderContext` consumes it to rebuild its viewport and render targets.

**Use-case:** Produced internally by `RenderContext.OnClientWindowChanged()` (and by `Game` when the OS window is resized) and stored until the next `RenderContext.Begin()` call, which applies it via `RefreshWindow()`. Game code rarely needs to construct one directly.

### ⭐ Constructors

```csharp
public WindowChangeSettings(Point size)
```

Creates settings requesting a resize to `size`, keeping `NativeResolution`, `ScalingKind`, and `Force` at their defaults.

**Parameters** \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties

#### Force

```csharp
public bool Force { get; init; }
```

When `true`, forces the viewport to rebuild even if `Size` and `NativeResolution` are unchanged from the current viewport. Used when something other than a resize (e.g. a scaling preference change) requires a refresh. Defaults to `false`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### NativeResolution

```csharp
public Point? NativeResolution { get; init; }
```

The native (design) resolution the game should be scaled from. When `null`, `Game.DefaultWidth`/`Game.DefaultHeight` are used instead. Defaults to `null`.

**Returns** \
[Point?](../../../Murder/Core/Geometry/Point.html) \

#### ScalingKind

```csharp
public ScalingKind ScalingKind { get; init; }
```

How the native resolution should be scaled to fit `Size` (e.g. auto-fit, integer scaling). Defaults to `ScalingKind.Auto`.

**Returns** \
[ScalingKind](../../../Murder/Save/ScalingKind.html) \

#### Size

```csharp
public Point Size;
```

The new client window size, in pixels.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

⚡

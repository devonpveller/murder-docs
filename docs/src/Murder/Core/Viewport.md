# Viewport

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct Viewport
```

Computes and stores how the game's native rendering resolution maps onto the actual window/screen size for a given `ScalingKind` strategy.

**Intent:** Derives the resulting integer/fractional `Scale` factor, the letterboxed `OutputRectangle` the game should be drawn into, and (for some scaling modes) an adjusted `NativeResolution`. This is a pure, immutable calculation — constructing a new `Viewport` re-derives every field from the three constructor arguments; nothing is mutated after construction.

**Use-case:** Queried by the render context and camera systems to determine where to draw the game's output rectangle and how to map screen-space coordinates to world space. Recompute a `Viewport` (e.g. from `GamePreferences.SetScalingKind` or a window-resize handler) whenever the window size or the user's `ScalingKind` preference changes.

### ⭐ Constructors

```csharp
public Viewport(Point viewportSize, Point nativeResolution, ScalingKind scaling)
```

Computes a `Viewport` mapping `nativeResolution` onto a window of `viewportSize` using the given `scaling` strategy. Different `ScalingKind` values produce very different results: `OneX`/`TwoX`/`ThreeX` pin the scale to an exact integer and center the (unscaled) native resolution; `Auto`/`Large` shrink the native resolution based on the window height before auto-scaling and snapping to a near-integer scale; `Snap` clamps the native resolution's aspect ratio to a sane range before stretching and snapping.

**Parameters** \
`viewportSize` [Point](../../Murder/Core/Geometry/Point.html) \
`nativeResolution` [Point](../../Murder/Core/Geometry/Point.html) \
`scaling` [ScalingKind](../../Murder/Save/ScalingKind.html) \

### ⭐ Properties

#### Center

```csharp
public readonly Vector2 Center;
```

The center point of `NativeResolution` (half its width/height), useful as a default camera focus point.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### FailedConstraints

```csharp
public readonly bool FailedConstraints;
```

Reserved flag intended to signal that the requested scaling constraints couldn't be satisfied. The constructor never actually sets this to `true` today, so it's always `false` for any `Viewport` built by the current implementation.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### NativeResolution

```csharp
public readonly Point NativeResolution;
```

The resolution that the game is actually rendered

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### OriginalScale

```csharp
public readonly Vector2 OriginalScale;
```

The scale resulting in viewportSize/nativeResolution without any snapping.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### OutputRectangle

```csharp
public readonly IntRectangle OutputRectangle;
```

The rectangle where the game should be rendered on the screen.

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### Scale

```csharp
public readonly Vector2 Scale;
```

The scale that is applied to the native resolution before rendering

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Size

```csharp
public readonly Point Size;
```

The size of the viewport (typically the game's window)

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

⚡

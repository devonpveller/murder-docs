# Calculator

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class Calculator
```

Calculator helper class.

**Intent:** The engine's general-purpose math toolbox: array/list helpers, geometry and intersection tests, angle and interpolation math, layer-depth conversions, deterministic (seeded) random helpers, and easing-adjacent time-normalization functions. Almost every gameplay system that needs to lerp, clamp, snap, or convert a value goes through this class instead of re-deriving the formula inline.

**Use-case:** Use in game systems and components for clamping, lerping, rounding, grid conversions, deterministic pseudo-random values, spring/smoothing motion, and other frequently needed math operations. Prefer these over hand-rolled equivalents so behavior (rounding rules, epsilon handling, wrap-around semantics) stays consistent across the codebase.

### ⭐ Properties

#### LayersCount

```csharp
public static int LayersCount;
```

The total number of distinct render/sorting layers the engine supports (65536, i.e. 16 bits, covering the range [-32768, 32768]). It is the denominator used by `ConvertLayerToLayerDepth`/`ConvertLayerDepthToLayer` to map an integer layer index onto the `[0, 1]` sprite-batch `layerDepth` value MonoGame uses for draw ordering. Marked with a `TODO` in source to become configurable, but currently a fixed global.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### TO_DEG

```csharp
public static const float TO_DEG;
```

Conversion factor from radians to degrees (180 ÷ π). Multiply a radian value by this constant to get degrees.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TO_RAD

```csharp
public static const float TO_RAD;
```

Conversion factor from degrees to radians (π ÷ 180). Multiply a degree value by this constant to get radians.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### AlmostEqual(float, float)

```csharp
public bool AlmostEqual(float num1, float num2)
```

Returns `true` if `num1` and `num2` differ by no more than `float.Epsilon`. Because `float.Epsilon` is the smallest representable positive float (not a "reasonable" tolerance), this only catches values that are effectively bit-identical — use `SameSignOrSimilar` or a custom threshold comparison for looser equality checks.

**Parameters** \
`num1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`num2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Blink(float, bool)

```csharp
public bool Blink(float speed, bool scaled)
```

Returns a boolean that alternates on/off at the given `speed` (cycles per second), driven by `Game.Now` (if `scaled` is `true`) or `Game.NowUnscaled` otherwise. Useful for blinking sprites, UI prompts, or "flash on hit" effects that should (or should not) pause with slow-motion/time-scale effects.

**Parameters** \
`speed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`scaled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Blink(float, float)

```csharp
public bool Blink(float speed, float time)
```

Overload of `Blink(float, bool)` that takes an explicit `time` value instead of reading it from `Game`, so callers can drive the blink from a custom clock (e.g. an entity's own elapsed-time field).

**Parameters** \
`speed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`time` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DistanceCheck(Vector2, Vector2, float)

```csharp
public bool DistanceCheck(Vector2 a, Vector2 b, float distance)
```

Returns `true` if the distance between `a` and `b` is less than or equal to `distance`. Compares squared lengths internally, so it avoids a costly `Sqrt` call — prefer this over computing `Vector2.Distance(a, b) <= distance` by hand in hot code such as proximity/AI-range checks.

**Parameters** \
`a` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`b` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`distance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DistanceCheck(float, float, float)

```csharp
public bool DistanceCheck(float a, float b, float distance)
```

Scalar overload of `DistanceCheck`: returns `true` if `|a - b|` is less than or equal to `distance`.

**Parameters** \
`a` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`b` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`distance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsInteger(float)

```csharp
public bool IsInteger(float value)
```

Returns `true` if the float value has no fractional part.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsInteger(Vector2)

```csharp
public bool IsInteger(Vector2 value)
```

Returns `true` if both components of the vector have no fractional part.

**Parameters** \
`value` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LineSegmentsIntersect(Vector2, Vector2, Vector2, Vector2)

```csharp
public bool LineSegmentsIntersect(Vector2 p1, Vector2 p2, Vector2 p3, Vector2 p4)
```

Returns `true` if segment `p1`–`p2` intersects segment `p3`–`p4`. Allocation-free equivalent to the intersection test on `Line2`, intended for use in tight loops (e.g. line-of-sight or path-clipping checks against many candidate segments). Parallel/collinear segments are treated as non-intersecting for performance, which is an accepted trade-off since exact collinear overlaps are rare in gameplay code.

**Parameters** \
`p1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`p2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`p3` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`p4` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SameSign(float, float)

```csharp
public bool SameSign(float num1, float num2)
```

Returns `true` if both values have the same sign (both positive or both negative); either value being exactly zero counts as a match.

**Parameters** \
`num1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`num2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SameSignOrSimilar(float, float)

```csharp
public bool SameSignOrSimilar(float num1, float num2)
```

Returns `true` if both values have the same sign or are close enough to zero (within `float.Epsilon`) to be treated as the same.

**Parameters** \
`num1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`num2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### MultiplyUnsigned8Bit(byte, int)

```csharp
public byte MultiplyUnsigned8Bit(byte a, int b)
```

Returns the result of multiplying an 8-bit value `a` by `b` using fixed-point integer math (with `0x80` rounding) rather than floating point, matching how many color/alpha-multiplication algorithms round 8-bit channel values.

**Parameters** \
`a` [byte](https://learn.microsoft.com/en-us/dotnet/api/System.Byte?view=net-7.0) \
`b` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[byte](https://learn.microsoft.com/en-us/dotnet/api/System.Byte?view=net-7.0) \

#### LerpSnap(float, float, double, float)

```csharp
public double LerpSnap(float origin, float target, double factor, float threshold)
```

Interpolates from `origin` to `target` by `factor`; snaps directly to `target` when the remaining distance is less than `threshold`. This `double`-factor overload exists for callers accumulating interpolation factors in double precision to avoid drift.

**Parameters** \
`origin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`target` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`factor` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \
`threshold` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \

#### ApproachAngle(float, float, float)

```csharp
public float ApproachAngle(float initialAngle, float targetAngle, float maxAngle)
```

Approaches from `initialAngle` to `targetAngle` by at most `maxAngle` radians, taking the shortest circular path (wrapping through ±π rather than always going the "long way"). Use for smoothly turning a facing/aim angle toward a target without overshooting or spinning the wrong direction.

**Parameters** \
`initialAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`targetAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`maxAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Approach(float, float, float)

```csharp
public float Approach(float from, float target, float amount)
```

Moves `from` toward `target` by at most `amount`, never overshooting. The workhorse for frame-based "move value toward target at a fixed rate" logic (health regen, camera zoom, volume fades, etc.).

**Parameters** \
`from` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`target` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### CatmullRom(float, float, float, float, float)

```csharp
public float CatmullRom(float p0, float p1, float p2, float p3, float t)
```

Evaluates a Catmull-Rom spline at parameter `t` using the four control points `p0`–`p3` (`p1`/`p2` are the segment endpoints, `p0`/`p3` provide tangent context). Used internally by the `Curve` overloads to smoothly interpolate through a list of keyframe values.

**Parameters** \
`p0` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`p1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`p2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`p3` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`t` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ClampAngle(float, float, float)

```csharp
public float ClampAngle(float angle, float center, float range)
```

Clamps `angle` (radians) to within `range / 2` of `center`, wrapping correctly across the ±π boundary. Use to restrict a turret's or camera's rotation to a limited arc around a rest angle.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`center` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`range` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ClampNearZero(float, float)

```csharp
public float ClampNearZero(float value, float minimum)
```

If `value`'s magnitude is smaller than `minimum`, snaps it to `±minimum` (sign-preserving); otherwise returns `value` unchanged. Useful for preventing a velocity or spring value from decaying into an imperceptible-but-nonzero "never quite stops" state.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`minimum` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ClampTime(float, float, float)

```csharp
public float ClampTime(float start, float now, float duration)
```

Convenience overload of `ClampTime(float, float)` that computes `elapsed` as `now - start` before normalizing it against `duration`.

**Parameters** \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`now` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ClampTime(float, float)

```csharp
public float ClampTime(float elapsed, float duration)
```

Normalizes the given elapsed time to a range of 0 to 1 based on the specified maximum time. If `duration` is 0, returns 1 immediately (treated as "already complete") to avoid a division by zero. This is the standard building block for progress/animation timers: pass `Game.Now - startTime` as `elapsed`.

**Parameters** \
`elapsed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ClampTime(float, float, float, float)

```csharp
public float ClampTime(float elapsed, float inDuration, float delayDuration, float outDuration)
```

Normalizes elapsed time to a 0-1 range across three phases — ramp in (`inDuration`), hold at 1 (`delayDuration`), ramp back out (`outDuration`) — so the returned value goes 0 → 1 → 0. Handy for effects that fade in, stay visible, then fade out (tooltips, damage numbers, screen flashes) without needing separate timers for each phase.

**Parameters** \
`elapsed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`inDuration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`delayDuration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`outDuration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ClampTime(float, float, EaseKind)

```csharp
public float ClampTime(float elapsed, float maxTime, EaseKind ease)
```

Normalizes elapsed time into 0-1 via `ClampTime(float, float)` and then runs it through `Ease.Evaluate` with the given `ease` curve, so animation progress can be eased without a separate `Ease` call at every call site.

**Parameters** \
`elapsed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`maxTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`ease` [EaseKind](../../Murder/Utilities/EaseKind.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ConvertLayerToLayerDepth(int)

```csharp
public float ConvertLayerToLayerDepth(int layer)
```

Converts an integer sorting `layer` (relative to `LayersCount`) into the normalized `[0, 1]` `layerDepth` value MonoGame's sprite batch uses for draw-order sorting. Pairs with `ConvertLayerDepthToLayer` for the inverse conversion; used wherever gameplay code exposes a human-friendly integer layer but needs to feed a float depth to rendering.

**Parameters** \
`layer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Curve(IList\<T\>, float)

```csharp
public float Curve(IList<T> values, float t)
```

Evaluates a smooth Catmull-Rom curve through the ordered `values` at normalized position `t ∈ [0, 1]`, clamping the neighboring control points at the ends of the list. This method was previously (and incorrectly) documented as `InterpolateSmoothCurve`; the current source names it `Curve`.

**Parameters** \
`values` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \
`t` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Curve(float, Single[])

```csharp
public float Curve(float delta, Single[] values)
```

`params`-array overload of `Curve(IList<T>, float)` so callers can pass keyframe values inline (e.g. `Calculator.Curve(t, 0f, 1f, 0.5f, 0f)`) instead of building a list first.

**Parameters** \
`delta` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`values` [float[]](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Curve(float, float, float, float)

```csharp
public float Curve(float delta, float start, float middle, float end)
```

Faster shorthand for the common three-keyframe case (`start` → `middle` → `end`): plain linear interpolation across each half rather than a full Catmull-Rom evaluation. Prefer this over the array-based `Curve` overloads when you only ever need three keyframes, since it avoids the array allocation/indexing overhead.

**Parameters** \
`delta` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`middle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`end` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DeltaAngle(float, float)

```csharp
public float DeltaAngle(float initialDirection, float angle)
```

Returns the shortest signed difference between `angle` and `initialDirection`, wrapped to `[-π, π]`. Use to find how far (and in which rotational direction) to turn from one angle to another.

**Parameters** \
`initialDirection` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DeterministicFloat(int, float, float)

```csharp
public float DeterministicFloat(int seed, float min, float max)
```

Hashes `seed` into a repeatable pseudo-random float in `[min, max)`. Unlike `Random`-based helpers, the same `seed` always produces the same output, which is essential for gameplay that must replay identically (e.g. per-entity visual jitter that shouldn't change between frames just because it was recomputed).

**Parameters** \
`seed` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DistancePointToLine(Vector2, Vector2, Vector2)

```csharp
public float DistancePointToLine(Vector2 point, Vector2 lineStart, Vector2 lineEnd)
```

Returns the shortest distance from `point` to the segment `lineStart`–`lineEnd` (clamped to the segment, not the infinite line). Built on `ClosestPointOnSegment` internally in spirit — used for things like measuring how far an entity has strayed from a patrol path.

**Parameters** \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`lineStart` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`lineEnd` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Lerp(float, float, float)

```csharp
public float Lerp(float origin, float target, float factor)
```

Standard linear interpolation: `origin + (target - origin) * factor`. The building block most other interpolation helpers in this class (`LerpInt`, `Lerp(Vector2, ...)`, `Curve`) are expressed in terms of.

**Parameters** \
`origin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`target` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`factor` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LerpSmooth(float, float, float, float)

```csharp
public float LerpSmooth(float a, float b, float deltaTime, float halfLife)
```

Smoothly interpolates between two float values over time using an exponential decay formula. It is similar to a regular linear interpolation (lerp) but is designed to work effectively even when not using a fixed timestep, making it particularly useful for smooth transitions in animations or physics simulations where the update interval can vary. `halfLife` controls how long it takes to close half the remaining distance to `b`.

**Parameters** \
`a` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`b` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`deltaTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`halfLife` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LerpSmoothAngle(float, float, float, float)

```csharp
public float LerpSmoothAngle(float a, float b, float deltaTime, float halfLife)
```

`LerpSmooth`-style exponential smoothing for angles: normalizes both angles first and takes the shortest rotational path around the circle before smoothing, so it never spins the "long way" the way a naive `LerpSmooth` on raw radians would.

**Parameters** \
`a` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`b` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`deltaTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`halfLife` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LerpSmoothSnap(float, float, float, float, float)

```csharp
public float LerpSmoothSnap(float current, float target, float deltaTime, float halfLife, float threshold)
```

`LerpSmooth` variant that snaps directly to `target` once the remaining distance drops below `threshold`, avoiding the "asymptotically never quite arrives" behavior inherent to exponential decay.

**Parameters** \
`current` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`target` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`deltaTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`halfLife` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`threshold` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LerpSnap(float, float, float, float)

```csharp
public float LerpSnap(float origin, float target, float factor, float threshold)
```

Linearly interpolates from `origin` to `target` by `factor`, but snaps straight to `target` once the two values are within `threshold` of each other — avoids a lerp chain that visually never quite settles.

**Parameters** \
`origin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`target` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`factor` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`threshold` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### NormalizeAngle(float)

```csharp
public float NormalizeAngle(float angle)
```

Normalizes the given angle to be within the range of 0 to 2π radians.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Parabola(float, float)

```csharp
public float Parabola(float x, float shape)
```

Maps a value within the range [0, 1] to a parabolic shape, where the corners are mapped to 0 and the center is mapped to 1. `shape` (typically `[0.5, 3]`) controls the sharpness of the curve — values below 1 widen and flatten it, values above 1 make it sharper and more peaked. Useful for arcs, jump heights, or any "rises then falls" envelope shaped by a single parameter.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`shape` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### PowerCurve(float, float, float)

```csharp
public float PowerCurve(float x, float a, float b)
```

Maps a value within the range [0, 1] to a power curve shape, where the corners are mapped to 0, with the rise (`a`) and fall (`b`) shapes controlled independently — a more flexible, asymmetric cousin of `Parabola`. Each of `a`/`b` (typically `[0.5, 3]`) makes its side of the curve steeper (below 1) or more gradual (above 1).

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`a` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`b` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Quantize(float, int)

```csharp
public float Quantize(float value, int steps)
```

Quantizes a float value to the nearest step defined by the number of steps. For example, if `steps` is 4, the value will be quantized to the nearest 0.25 (1/4). If `steps` is 10, the value will be quantized to the nearest 0.1 (1/10). Use to snap a continuous value (e.g. a slider or free-aim angle) onto a discrete grid.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`steps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Remap(float, float, float, float, float)

```csharp
public float Remap(float input, float inputMin, float inputMax, float min, float max)
```

Linearly remaps `input` from the range `[inputMin, inputMax]` to the range `[min, max]`. The general-purpose "convert this value from one scale to another" helper (e.g. converting a raw sensor/analog-stick reading into a gameplay-relevant range).

**Parameters** \
`input` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`inputMin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`inputMax` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Remap(float, float, float)

```csharp
public float Remap(float input, float min, float max)
```

Shorthand for `Remap(input, 0, 1, min, max)`: maps a normalized `[0, 1]` `input` into `[min, max]`.

**Parameters** \
`input` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### RemapAmplitude(float)

```csharp
public float RemapAmplitude(float value)
```

Remaps a value from the range [-1, 1] to [0, 1]. Handy for converting a signed oscillation (e.g. the output of `MathF.Sin`) into a normalized amplitude usable for alpha, volume, or scale.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Sine01(float)

```csharp
public float Sine01(float value)
```

Like sine but normalized between 0 and 1 instead of -1 and 1.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SmoothStep(float, float, float)

```csharp
public float SmoothStep(float value, float min, float max)
```

Clamps `value` to `[min, max]`, normalizes it, and applies the classic smoothstep curve (`3t² - 2t³`) for an ease-in/ease-out transition. Note the result is inverted relative to most smoothstep implementations (it returns `1` at `min` and `0` at `max` unless `min`/`max` are swapped, which flips the invert flag) — check call sites before assuming standard orientation.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SnapAngle(float, int)

```csharp
public float SnapAngle(float finalAngle, int steps)
```

Snap the current angle into `steps` degrees.

**Parameters** \
`finalAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`steps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ToSpringOscillation(float, float)

```csharp
public float ToSpringOscillation(float t, float frequency)
```

Converts a value to a spring oscillation. `t` is the "energy" of the spring (1 = fully oscillating, 0 or below = stopped); `frequency` controls how fast it oscillates. The result decays exponentially as `t` approaches 0, mimicking a damped spring settling to rest — used for squash/stretch or camera-shake style effects.

**Parameters** \
`t` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`frequency` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Wave(float, bool)

```csharp
public float Wave(float speed, bool scaled)
```

Generates a normalized sine wave value oscillating between 0 and 1, driven by `Game.Now` (`scaled = true`) or `Game.NowUnscaled` (`scaled = false`). Use for continuous pulsing effects (glow, breathing UI elements) that don't need explicit per-caller time tracking.

**Parameters** \
`speed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`scaled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Wave(float, float, float, bool)

```csharp
public float Wave(float speed, float min, float max, bool scaled)
```

`Wave(float, bool)` variant that scales the oscillation into `[min, max]` instead of a fixed `[0, 1]` range.

**Parameters** \
`speed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`scaled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### WrapAngle(float)

```csharp
public float WrapAngle(float angle)
```

Wraps an arbitrary angle in radians into the range `[-π, π]`, preserving its effective direction. Used by `ApproachAngle`/`DeltaAngle` to compute shortest-path rotations.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### WrapAround(float, float, float)

```csharp
public float WrapAround(float value, float min, float max)
```

Float overload of `WrapAround(int, int, int)`: wraps `value` into the `[min, max]` range using modulo arithmetic that stays correct for negative inputs (unlike a plain `%`). If `max < min`, returns `min`.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`min` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### CeilingToInt(float)

```csharp
public int CeilingToInt(float v)
```

Equivalent to `CeilToInt`: rounds `v` up and converts it to an `int`. Both methods exist in source with identical implementations — prefer `CeilToInt` for new code as the shorter, more consistently-used name.

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### CeilToInt(float)

```csharp
public int CeilToInt(float v)
```

Rounds `v` up with `MathF.Ceiling` and converts it to an `int`.

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ConvertLayerDepthToLayer(float)

```csharp
public int ConvertLayerDepthToLayer(float layerDepth)
```

Inverse of `ConvertLayerToLayerDepth`: converts a normalized `[0, 1]` sprite-batch `layerDepth` back into an integer sorting layer index.

**Parameters** \
`layerDepth` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DeterministicInt(int, int, int)

```csharp
public int DeterministicInt(int seed, int min, int max)
```

Hashes `seed` into a repeatable pseudo-random integer in `[min, max)`, using a large-prime multiply to mix the seed bits. Like `DeterministicFloat`, this is deterministic given the same `seed` — use for stable-per-entity "random" choices that must reproduce identically across runs/replays. Throws `ArgumentOutOfRangeException` if `max < min`.

**Parameters** \
`seed` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`min` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`max` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Exceptions** \
[ArgumentOutOfRangeException](https://learn.microsoft.com/en-us/dotnet/api/System.ArgumentOutOfRangeException?view=net-7.0) — thrown when `max` is less than `min`. \

#### Digits(int)

```csharp
public int Digits(int number)
```

Returns the number of base-10 digits in `number` (treating 0 as having 1 digit, and ignoring sign). Useful for formatting/layout code that needs to know how wide a number will render before drawing it.

**Parameters** \
`number` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### FloorOrCeilFromThreshold(float, float)

```csharp
public int FloorOrCeilFromThreshold(float v, float threshold)
```

Returns 0 if `v` is not positive; otherwise floors `v` if it's below `threshold`, or ceils it otherwise. A hybrid rounding rule for cases where small values should round down (to avoid prematurely triggering something) but larger values should round up.

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`threshold` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### FloorToInt(float)

```csharp
public int FloorToInt(float v)
```

Rounds `v` down with `MathF.Floor` and converts it to an `int`.

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### LerpInt(float, float, float)

```csharp
public int LerpInt(float origin, float target, float factor)
```

Linearly interpolates between `origin` and `target` by `factor`, rounding the result to the nearest `int` via `RoundToInt`.

**Parameters** \
`origin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`target` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`factor` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ManhattanDistance(Point, Point)

```csharp
public int ManhattanDistance(Point point1, Point point2)
```

Returns the Manhattan (grid/taxicab) distance between two `Point`s: `|dx| + |dy|`. Common for tile-grid heuristics such as A* pathfinding cost estimates.

**Parameters** \
`point1` [Point](../../Murder/Core/Geometry/Point.html) \
`point2` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### OneD(Point, int)

```csharp
public int OneD(Point p, int width)
```

Extension method that flattens a 2D grid `Point` into a 1D index (`p.X + p.Y * width`) for use as a key into a flat array-backed grid.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### OneD(int, int, int)

```csharp
public int OneD(int x, int y, int width)
```

Non-extension overload of `OneD(Point, int)` that takes raw `x`/`y` coordinates instead of a `Point`.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### PolarSnapToInt(float)

```csharp
public int PolarSnapToInt(float v)
```

Rounds `v` away from zero to the nearest integer magnitude while preserving its sign (equivalent to "ceiling of the absolute value, then re-apply sign"). Ensures small nonzero values never round down to 0 and lose their direction.

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Pow(int, int)

```csharp
public int Pow(int x, int y)
```

Computes `x` raised to the (non-negative) integer power `y` using fast exponentiation by squaring, avoiding the `double` round-trip that `Math.Pow` would require for an all-integer computation.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RoundToEven(float)

```csharp
public int RoundToEven(float v)
```

Rounds `v / 2` away from zero and doubles it, producing the nearest even integer to `v`. Used where a value must land on an even grid cell/pixel boundary.

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RoundToInt(double)

```csharp
public int RoundToInt(double v)
```

`double` overload of `RoundToInt(float)`; converts to `float` and delegates to it.

**Parameters** \
`v` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RoundToInt(float)

```csharp
public int RoundToInt(float v)
```

Rounds and converts a number to integer with [MathF.Round(System.Single)](https://learn.microsoft.com/en-us/dotnet/api/System.MathF?view=net-7.0).

**Parameters** \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### WrapAround(int, int, int)

```csharp
public int WrapAround(int value, int min, int max)
```

Wraps `value` into the inclusive `[min, max]` range, correctly handling negative inputs (a plain `%` would return a negative remainder in that case). If `max < min`, returns `min`. Common for cycling a selection index or a hue value that should loop back around at its ends.

**Parameters** \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`min` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`max` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ParsePixelSize(string)

```csharp
public Point ParsePixelSize(string size)
```

Parses a free-form pixel-size string such as `"800x600"`, `"800, 600"`, or `"800 600"` into a `Point`. Strips everything except digits, commas, spaces, and `x` before splitting, so it tolerates loosely-formatted user/config input; falls back to `800x600` if parsing fails.

**Parameters** \
`size` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### AddOnce(IList\<T\>, T)

```csharp
public T AddOnce(IList<T> list, T item)
```

Add `item` to `list`. Skip if already present. Cost O(n) (uses `Contains`, so it is only appropriate for small lists — not a substitute for a `HashSet` in hot paths).

**Parameters** \
`list` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \
`item` [T](../../) \

**Returns** \
[T](../../) \

#### TryGet(IList\<T\>, int)

```csharp
public T? TryGet(IList<T> values, int index)
```

Extension method that safely indexes into `values`, returning `null` instead of throwing if `index` is out of bounds. Constrained to `T : struct` so the `null` sentinel can be represented via `Nullable<T>`. Use when reading a possibly-short list by a computed index (e.g. an animation frame array) without a manual bounds check at every call site.

**Parameters** \
`values` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### TryGet(ImmutableArray\<T\>, int)

```csharp
public T? TryGet(ImmutableArray<T> values, int index)
```

`ImmutableArray<T>` overload of `TryGet(IList<T>, int)` with identical bounds-safe behavior.

**Parameters** \
`values` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### RepeatingArray(T, int)

```csharp
public T[] RepeatingArray(T value, int size)
```

Allocates a new array of `size` elements, all set to `value`. Shorthand for "allocate + `Populate`" in one call.

**Parameters** \
`value` [T](../../) \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T[]](../../) \

#### DetailedClosestPointOnSegment(Vector2, Vector2, Vector2)

```csharp
public ValueTuple<T1, T2> DetailedClosestPointOnSegment(Vector2 point, Vector2 a, Vector2 b)
```

Like `ClosestPointOnSegment`, but also returns the clamped projection factor `delta ∈ [0, 1]` along the segment (0 = at `a`, 1 = at `b`) as `(Vector2 point, float delta)`. Use when you need to know *where along* the segment the closest point falls, not just its coordinates (e.g. to interpolate a value stored per-endpoint).

**Parameters** \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`a` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`b` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### Spring(float, float, float, float, float, float)

```csharp
public ValueTuple<T1, T2> Spring(float value, float velocity, float targetValue, float damping, float frequency, float deltaTime)
```

Advances a semi-implicit damped spring simulation by one step and returns the new `(value, velocity)` pair. `targetValue` is the resting position, `damping`/`frequency` shape the spring's stiffness and settle behavior. Call every frame with the previous frame's returned `(value, velocity)` fed back in to drive spring-based motion (recoil, camera follow, UI element bounce) that reacts naturally to a moving target.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`velocity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`targetValue` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`damping` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`frequency` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`deltaTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### Approach(Vector2, Vector2, float)

```csharp
public Vector2 Approach(in Vector2 from, in Vector2 target, float amount)
```

Vector2 overload of `Approach(float, float, float)`: moves `from` toward `target` by at most `amount` units, never overshooting past `target`.

**Parameters** \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ClosestPointOnSegment(Vector2, Vector2, Vector2)

```csharp
public Vector2 ClosestPointOnSegment(Vector2 point, Vector2 a, Vector2 b)
```

Projects `point` onto the segment `a`–`b`, clamped so the result always lies between the two endpoints (never on the infinite line extension). Standard building block for point-vs-line collision and steering-toward-a-path logic.

**Parameters** \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`a` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`b` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### DeterministicVector2(int, float)

```csharp
public Vector2 DeterministicVector2(int seed, float radius)
```

Hashes `seed` into a repeatable pseudo-random offset vector scaled by `radius` (each axis independently hashed, so the result is not uniformly distributed within a circle — use `DeterministicVector2InACircle` for that). Deterministic given the same `seed`.

**Parameters** \
`seed` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### DeterministicVector2InACircle(int, float)

```csharp
public Vector2 DeterministicVector2InACircle(int seed, float radius)
```

Hashes `seed` into a repeatable pseudo-random point uniformly distributed inside a circle of the given `radius` (uses a square-root distance distribution to avoid center-clustering). Deterministic given the same `seed` — use for stable per-entity scatter/jitter positions (e.g. particle spawn offsets that must match across a replay).

**Parameters** \
`seed` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetPositionInSemicircle(float, Vector2, float, float, float)

```csharp
public Vector2 GetPositionInSemicircle(float ratio, Vector2 center, float radius, float startAngle, float endAngle)
```

Returns the point at normalized position `ratio ∈ [0, 1]` along an arc of the given `radius` around `center`, sweeping from `startAngle` to `endAngle` (both in degrees). Despite the name, it works for any arc, not just semicircles — used to lay out UI elements or projectiles along a curved arrangement.

**Parameters** \
`ratio` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`endAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Lerp(Vector2, Vector2, float)

```csharp
public Vector2 Lerp(Vector2 origin, Vector2 target, float factor)
```

Component-wise `Lerp(float, float, float)` applied to both axes of `origin`/`target`.

**Parameters** \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`factor` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### LerpSmooth(Vector2, Vector2, float, float)

```csharp
public Vector2 LerpSmooth(Vector2 current, Vector2 target, float deltaTime, float halfLife)
```

Smoothly interpolates between two vectors over time using a linear interpolation method. It interpolates each component of the vector individually using `LerpSmooth(float, float, float, float)`. It is similar to a regular linear interpolation (lerp) but is designed to work effectively even when not using a fixed timestep, which makes it particularly useful for smooth transitions in animations or physics simulations where the update interval can vary — this is the go-to helper for smooth camera-follow and cursor-trailing motion.

**Parameters** \
`current` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`deltaTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`halfLife` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### LerpSmoothSnap(Vector2, Vector2, float, float, float)

```csharp
public Vector2 LerpSmoothSnap(Vector2 current, Vector2 target, float deltaTime, float halfLife, float threshold)
```

Component-wise `LerpSmoothSnap(float, float, float, float, float)` applied to both axes — smoothly interpolates each axis and snaps directly to `target` once within `threshold`.

**Parameters** \
`current` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`deltaTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`halfLife` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`threshold` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### LerpSnap(Vector2, Vector2, float, float)

```csharp
public Vector2 LerpSnap(Vector2 origin, Vector2 target, float factor, float threshold = 0.01f)
```

Component-wise `LerpSnap(float, float, float, float)` applied to both axes of `origin`/`target`.

**Parameters** \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`factor` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`threshold` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Normalized(Vector2)

```csharp
public Vector2 Normalized(in Vector2 vector2)
```

Extension method returning a normalized copy of `vector2`. Note the implementation calls the mutating `Vector2.Normalized()` extension (see `Vector2Extensions`) on a local copy and then returns that copy — it does not mutate the caller's vector.

**Parameters** \
`vector2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### RandomPointInCircleEdge()

```csharp
public Vector2 RandomPointInCircleEdge()
```

Returns a random unit-length point on the edge (circumference) of a unit circle, using `Random.Shared`. Not deterministic — use `DeterministicVector2InACircle` if reproducibility is required.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### RandomPointInRectangle(IntRectangle)

```csharp
public Vector2 RandomPointInRectangle(IntRectangle rectangle)
```

Returns a random point uniformly distributed within `rectangle`'s bounds, using `Random.Shared`. Not deterministic.

**Parameters** \
`rectangle` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### RandomPointInsideCircle()

```csharp
public Vector2 RandomPointInsideCircle()
```

Returns a random point uniformly distributed inside a unit circle (radius 1), using `Random.Shared`. Not deterministic — use `DeterministicVector2InACircle` if reproducibility is required.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Populate(T[], T)

```csharp
public void Populate(T[] arr, T value)
```

Extension method that fills every element of `arr` with `value` in place.

**Parameters** \
`arr` [T[]](../../) \
`value` [T](../../) \

⚡

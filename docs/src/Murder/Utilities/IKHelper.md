# IKHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class IKHelper
```

Two-bone inverse-kinematics (IK) helpers for a simple base-elbow-end chain (e.g. an arm or leg made of two segments), computing where the "elbow" joint should be positioned so the chain reaches from a fixed base to a target end position.

**Intent:** Provides the standard Law-of-Cosines two-bone IK solve (and safe/clamped variants of it) so procedural limb animation — pointing an arm at a target, having a leg reach for a foothold — doesn't need to be re-derived per project. Not currently called anywhere within the engine itself; it exists as a general-purpose utility for game code built on Murder.

**Use-case:** Call `GetElbowPosition` when you need to know whether a two-segment chain can physically reach a target and, if so, where its middle joint should be. Prefer `GetSafeElbowPosition` when you always need *some* pose, even if the target is out of reach (it clamps the target to the chain's valid range instead of returning `null`); use the `elbowTarget` overload when you want the elbow to consistently bend toward a preferred direction instead of flipping unpredictably as the target moves.

### ⭐ Methods

#### GetElbowPosition(Vector2, Vector2, float, float, bool)

```csharp
public Vector2? GetElbowPosition(Vector2 basePosition, Vector2 endPosition, float segmentLength1, float segmentLength2, bool flipElbow = false)
```

Computes the elbow position for a two-segment IK chain from `basePosition` to `endPosition` using the Law of Cosines, given the two segment lengths. Returns `null` if the target is unreachable — either farther away than the fully-extended chain (`segmentLength1 + segmentLength2`) or closer than the chain can fold to (`|segmentLength1 - segmentLength2|`). `flipElbow` selects between the two mirror-image solutions that satisfy the same base/end/lengths.

**Parameters** \
`basePosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`endPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`segmentLength1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`segmentLength2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`flipElbow` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Vector2?](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetSafeElbowPosition(Vector2, Vector2, float, float, bool)

```csharp
public Vector2 GetSafeElbowPosition(Vector2 basePosition, Vector2 endPosition, float segmentLength1, float segmentLength2, bool flipElbow = false)
```

Like `GetElbowPosition`, but never returns `null`: if `endPosition` is unreachable, it is first clamped to the nearest valid distance (either the fully-extended or fully-folded reach of the chain) before the elbow is computed, so the chain always resolves to a "best effort" pose that reaches as close to the real target as possible.

**Parameters** \
`basePosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`endPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`segmentLength1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`segmentLength2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`flipElbow` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetSafeElbowPosition(Vector2, Vector2, float, float, Vector2, bool)

```csharp
public Vector2 GetSafeElbowPosition(Vector2 basePosition, Vector2 endPosition, float segmentLength1, float segmentLength2, Vector2 elbowTarget, bool flipElbow = false)
```

Overload of `GetSafeElbowPosition` that computes both geometrically-valid elbow solutions and, when `flipElbow` is `false`, picks whichever one is closer to `elbowTarget` — a hint position used to keep the elbow bending toward a natural/preferred direction (e.g. always bending "forward") rather than flipping unpredictably as the end target moves. `endPosition` is clamped to the chain's maximum reach rather than treated as unreachable.

**Parameters** \
`basePosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`endPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`segmentLength1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`segmentLength2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`elbowTarget` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`flipElbow` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡

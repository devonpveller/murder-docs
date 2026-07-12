# FrameInfo

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct FrameInfo
```

A struct representing information about a single animation frame, such as its index in the list and a flag indicating whether the animation is complete.

**Intent:** Snapshot of the current playback state for a sprite animation at a given point in time, bundling the current frame index, the frame index scoped to the currently-playing `Animation`, and a completion flag together so callers don't need to query several separate values.

**Use-case:** Returned by animation update calls (e.g. sprite-playing systems and components that advance an `Animation` each frame) so callers can react to frame changes, know the current frame index for rendering, or detect when the animation has finished (to loop, transition to another animation, or destroy a one-shot effect entity). Use the static `Fail` value to signal that an animation lookup failed rather than returning a default/zeroed instance that could be mistaken for a valid frame 0.

### ⭐ Constructors

```csharp
public FrameInfo()
```

Creates a default `FrameInfo` at frame 0 with the animation marked as incomplete and no `Animation` set.

```csharp
public FrameInfo(Animation animation)
```

Creates a `FrameInfo` at frame 0 for the given animation, marking it as incomplete. Used to seed the initial state before any frames have been advanced.

**Parameters** \
`animation` [Animation](../../Murder/Core/Graphics/Animation.html) \

```csharp
public FrameInfo(int frame, int internalFrame, bool animationComplete, Animation animation)
```

Creates a fully specified `FrameInfo` with explicit frame indices, completion state, and associated animation. Used by animation-advancing code once it has computed the new frame state for the current tick.

**Parameters** \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`internalFrame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`animationComplete` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`animation` [Animation](../../Murder/Core/Graphics/Animation.html) \

### ⭐ Properties

#### Animation

```csharp
public Animation Animation { get; public set; }
```

The animation data associated with this frame snapshot, i.e. which `Animation` (frame list, frame rate, loop settings) is currently being played.

**Returns** \
[Animation](../../Murder/Core/Graphics/Animation.html) \

#### Complete

```csharp
public readonly bool Complete;
```

Whether the animation is complete. Check this to know when a non-looping animation has finished playing, e.g. to trigger a follow-up action or destroy a one-shot effect.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Fail

```csharp
public static FrameInfo Fail { get; }
```

A sentinel `FrameInfo` value whose `Failed` flag is set to `true`, used to signal that an animation lookup failed (e.g. the requested animation name does not exist on the sprite) without resorting to a nullable return type.

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### Failed

```csharp
public bool Failed { get; public set; }
```

Indicates whether this frame info represents a failed or invalid animation lookup (see `Fail`). Callers should check this before trusting `Frame`/`InternalFrame`/`Animation`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Frame

```csharp
public readonly int Frame;
```

The index of the current frame.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### InternalFrame

```csharp
public readonly int InternalFrame;
```

The index of the current frame inside the current animation.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

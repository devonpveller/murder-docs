# FrameInfo

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct FrameInfo
```

A struct representing information about a single animation frame, such as its index in the list and a flag indicating whether the animation is complete

**Intent:** Snapshot of the current playback state for a sprite animation at a given point in time.

**Use-case:** Returned by animation update calls so systems and components can react to frame changes, know the current frame index, or detect when the animation has finished.

### ⭐ Constructors
```csharp
public FrameInfo()
```

Creates a default `FrameInfo` at frame 0 with the animation marked as incomplete.

```csharp
public FrameInfo(Animation animation)
```

Creates a `FrameInfo` at frame 0 for the given animation, marking it as incomplete.

**Parameters** \
`animation` [Animation](../../Murder/Core/Graphics/Animation.html) \

```csharp
public FrameInfo(int frame, int internalFrame, bool animationComplete, Animation animation)
```

Creates a fully specified `FrameInfo` with explicit frame indices, completion state, and associated animation.

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

The animation data associated with this frame snapshot.

**Returns** \
[Animation](../../Murder/Core/Graphics/Animation.html) \
#### Complete
```csharp
public readonly bool Complete;
```

Whether the animation is complete

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Fail
```csharp
public static FrameInfo Fail { get; }
```

A sentinel `FrameInfo` value whose `Failed` flag is set to `true`, used to signal that animation lookup failed.

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \
#### Failed
```csharp
public bool Failed { get; public set; }
```

Indicates whether this frame info represents a failed or invalid animation lookup.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Frame
```csharp
public readonly int Frame;
```

The index of the current frame

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### InternalFrame
```csharp
public readonly int InternalFrame;
```

The index of the current frame inside the current animation

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
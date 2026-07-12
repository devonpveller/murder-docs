# AnimationOverloadProperties

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
[Flags]
public enum AnimationOverloadProperties : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Bit flags that configure how [EntityServices](../../Murder/Services/EntityServices.html)`.PlayAnimationOverload` builds the `AnimationOverloadComponent` it applies to an entity.

**Intent:** Lets callers describe a temporary animation override declaratively (loop or not, ignore facing or not, flip, lock to specific directions/orientations, or disappear at the end) instead of constructing an `AnimationOverloadComponent` by hand.

**Use-case:** Pass a combination of these flags to `PlayAnimationOverload` — for example `AnimationOverloadProperties.Loop | AnimationOverloadProperties.IgnoreFacing` (the default) for a looping effect that plays the same regardless of the entity's facing direction, or `Disappear` for a one-shot animation overlay that fades the entity out once it completes.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### None

```csharp
public static const AnimationOverloadProperties None;
```

No special behavior; the animation overload plays with none of the other flags' adjustments.

**Returns** \
[AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \

#### Loop

```csharp
public static const AnimationOverloadProperties Loop;
```

Marks the overload animation to loop on the resulting `AnimationOverloadComponent` instead of playing once.

**Returns** \
[AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \

#### IgnoreFacing

```csharp
public static const AnimationOverloadProperties IgnoreFacing;
```

Plays the overload animation the same way regardless of the entity's current facing direction, rather than picking a direction-suffixed variant.

**Returns** \
[AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \

#### FlipHorizontal

```csharp
public static const AnimationOverloadProperties FlipHorizontal;
```

Renders the overload animation horizontally mirrored (sets `ImageFlip.Horizontal` on the component).

**Returns** \
[AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \

#### LockTo4Directions

```csharp
public static const AnimationOverloadProperties LockTo4Directions;
```

Restricts the overload's supported directions to 4 (cardinal) instead of the entity's usual directional granularity, for animation sets that only have up/down/left/right variants.

**Returns** \
[AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \

#### Once

```csharp
public static const AnimationOverloadProperties Once;
```

Not implemented yet, per the source comment; reserved for a future "play exactly once" behavior distinct from `Loop`.

**Returns** \
[AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \

#### Disappear

```csharp
public static const AnimationOverloadProperties Disappear;
```

Combination flag (`Once | 0x100000`) that appends a terminating `"_"` frame to the played animation sequence and forces `Loop` on so playback ends by disappearing rather than looping visibly. Used for effects that should play once and vanish.

**Returns** \
[AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \

#### LockHorizontal

```csharp
public static const AnimationOverloadProperties LockHorizontal;
```

Constrains the overload's supported orientation to horizontal only (sets `SupportedOrientation` to `Orientation.Horizontal`).

**Returns** \
[AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \

#### LockVertical

```csharp
public static const AnimationOverloadProperties LockVertical;
```

Constrains the overload's supported orientation to vertical only (sets `SupportedOrientation` to `Orientation.Vertical`).

**Returns** \
[AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \

⚡

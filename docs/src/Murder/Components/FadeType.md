# FadeType

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed enum FadeType : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies the direction and style of a full-screen fade effect.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Tells the consuming fade renderer which fade algorithm to run so the screen overlay behaves correctly for the current transition context. Used by both [FadeScreenComponent](../../Murder/Components/FadeScreenComponent.html) (`Fade`, all four values) and [FadeScreenWithSolidColorComponent](../../Murder/Components/FadeScreenWithSolidColorComponent.html) (`FadeType`, which is only ever driven with `In`/`Out` by `FadeScreenWithSolidColorSystem`).

**Use-case:** Set on `FadeScreenComponent.Fade` or `FadeScreenWithSolidColorComponent.FadeType`; use `In` to fade from the overlay color to the scene, `Out` to fade the scene to the overlay color, `Flash` for a brief flash to a solid color and back, and `OutBuffer` for a fade-out that holds the overlay for `FadeScreenComponent.BufferFrames` extra frames before completing (avoids a one-frame gap during scene transitions).

### ⭐ Properties

#### Flash

```csharp
public static const FadeType Flash;
```

A brief flash to a solid color and back, used for hit-flashes or scene-entry punctuation.

**Returns** \
[FadeType](../../Murder/Components/FadeType.html) \

#### In

```csharp
public static const FadeType In;
```

Fades from the overlay color to fully transparent, revealing the scene.

**Returns** \
[FadeType](../../Murder/Components/FadeType.html) \

#### Out

```csharp
public static const FadeType Out;
```

Fades from transparent to the overlay color, covering the scene.

**Returns** \
[FadeType](../../Murder/Components/FadeType.html) \

#### OutBuffer

```csharp
public static const FadeType OutBuffer;
```

Fades out and then holds the overlay for `BufferFrames` extra frames before signaling completion, preventing single-frame rendering gaps during scene transitions.

**Returns** \
[FadeType](../../Murder/Components/FadeType.html) \

⚡

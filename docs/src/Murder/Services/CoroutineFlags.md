# CoroutineFlags

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public enum CoroutineFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Options that control how a coroutine started through [CoroutineServices](../../Murder/Services/CoroutineServices.html) behaves with respect to the game's pause state.

**Intent:** Lets callers opt a specific coroutine out of the normal pause behavior, without needing a separate "unpaused coroutine" API.

**Use-case:** Pass `CoroutineFlags.DoNotPause` to `RunCoroutine`, `FireAfter`, `FireNextFrame`, `FireAfterFrames`, or `FireForDuration` when the coroutine drives something that must keep running while gameplay is paused — for example a pause-menu animation, a fade transition into the pause screen itself, or other UI logic that should not freeze along with the simulation. Use the default `None` for ordinary gameplay coroutines that should stop advancing while the game is paused.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### None

```csharp
public static const CoroutineFlags None;
```

The default behavior: the coroutine pauses along with the rest of the game simulation.

**Returns** \
[CoroutineFlags](../../Murder/Services/CoroutineFlags.html) \

#### DoNotPause

```csharp
public static const CoroutineFlags DoNotPause;
```

Keeps the coroutine advancing even while the game is paused, for coroutines that drive pause-independent logic such as menu or transition animations.

**Returns** \
[CoroutineFlags](../../Murder/Services/CoroutineFlags.html) \

⚡

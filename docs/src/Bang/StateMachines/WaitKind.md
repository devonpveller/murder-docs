# WaitKind

**Namespace:** Bang.StateMachines \
**Assembly:** Bang.dll

```csharp
public sealed enum WaitKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Describes what condition a [StateMachine](../../Bang/StateMachines/StateMachine.html) should wait on before resuming a routine — i.e. the "kind" of a [Wait](../../Bang/StateMachines/Wait.html) value yielded from a state's `IEnumerator<Wait>` routine. `StateMachine`'s tick loop switches on this value to decide whether to start a timer, listen for a message, count frames, delegate to a nested routine, or stop entirely.

Game code does not normally construct a `WaitKind` directly — it is set implicitly by whichever [Wait](../../Bang/StateMachines/Wait.html) static factory method (`Wait.ForMs(int)`, `Wait.ForMessage<T>()`, `Wait.ForFrames(int)`, `Wait.ForRoutine(IEnumerator<Wait>)`, `Wait.Stop`, etc.) was used to create the `Wait` being `yield return`ed from a state.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Frames
```csharp
public static const WaitKind Frames;
```

Wait for 'x' frames. Produced by `Wait.ForFrames(int)`/`Wait.NextFrame`; the routine resumes after that many engine ticks have passed, regardless of elapsed time.

**Returns** \
[WaitKind](../../Bang/StateMachines/WaitKind.html) \
#### Message
```csharp
public static const WaitKind Message;
```

Wait for a message to be fired. Produced by the `Wait.ForMessage<T>` overloads; the routine resumes once a message of the requested type is sent to the target entity (or, if a timeout was given, once that timeout elapses — whichever comes first).

**Returns** \
[WaitKind](../../Bang/StateMachines/WaitKind.html) \
#### Ms
```csharp
public static const WaitKind Ms;
```

Wait for 'x' ms. Produced by `Wait.ForMs(int)`/`Wait.ForSeconds(float)`; the routine resumes once that many milliseconds have elapsed.

**Returns** \
[WaitKind](../../Bang/StateMachines/WaitKind.html) \
#### Routine
```csharp
public static const WaitKind Routine;
```

Redirect execution to another routine. This will resume once that's finished. Produced by `Wait.ForRoutine(IEnumerator<Wait>)`; lets one state's routine delegate to (and wait on) another `IEnumerator<Wait>` as a nested sub-routine.

**Returns** \
[WaitKind](../../Bang/StateMachines/WaitKind.html) \
#### Stop
```csharp
public static const WaitKind Stop;
```

Stops the state machine execution. Produced by `Wait.Stop`; once yielded, the routine is considered finished and the state machine component is torn down.

**Returns** \
[WaitKind](../../Bang/StateMachines/WaitKind.html) \


⚡

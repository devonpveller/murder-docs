# Wait

**Namespace:** Bang.StateMachines \
**Assembly:** Bang.dll

```csharp
public class Wait : IEquatable<T>
```

The value a [StateMachine](../../Bang/StateMachines/StateMachine.html) routine `yield return`s to tell the engine when it should be resumed. Every state method has the shape `IEnumerator<Wait> MyState()`; each `yield return` inside it hands one of these back to `StateMachine`, which suspends the routine until the condition described by [Kind](../../Bang/StateMachines/Wait.html#kind) is met, then resumes execution right after that `yield return`.

`Wait` is a C# `record`, so two `Wait` values with the same [Kind](../../Bang/StateMachines/Wait.html#kind)/[Value](../../Bang/StateMachines/Wait.html#value)/[Component](../../Bang/StateMachines/Wait.html#component)/[Target](../../Bang/StateMachines/Wait.html#target)/[Routine](../../Bang/StateMachines/Wait.html#routine) compare equal; that is incidental, however — instances are never created directly (all constructors are `private`). Instead, always build one through the static factory members below: [ForMs(int)](../../Bang/StateMachines/Wait.html#formsint) / [ForSeconds(float)](../../Bang/StateMachines/Wait.html#forsecondsfloat) to wait on a timer, [ForMessage()](../../Bang/StateMachines/Wait.html#formessage) and its overloads to wait on a message, [ForFrames(int)](../../Bang/StateMachines/Wait.html#forframesint) / [NextFrame](../../Bang/StateMachines/Wait.html#nextframe) to wait on ticks, [ForRoutine(IEnumerator\<T\>)](../../Bang/StateMachines/Wait.html#forroutineienumeratort) to delegate to a nested sub-routine, or [Stop](../../Bang/StateMachines/Wait.html#stop) to end the state machine. This keeps every `Wait` in circulation as one of the well-defined kinds in [WaitKind](../../Bang/StateMachines/WaitKind.html), which is what `StateMachine`'s tick loop switches on.

A typical routine mixes several of these, for example (from `Murder.StateMachines.Dialogs.DialogStateMachine.Talk`):

```csharp
yield return Wait.NextFrame;
yield return Wait.ForMessage<NextDialogMessage>();
```

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors
```csharp
protected Wait(Wait original)
```

Copy constructor synthesized by the compiler for the `record` type; not meant to be called directly by game code (all of `Wait`'s own constructors are `private`, and it is always created through the static factory members below).

**Parameters** \
`original` [Wait](../../Bang/StateMachines/Wait.html) \

### ⭐ Properties
#### Component
```csharp
public Type Component;
```

The message type being waited for, if [Kind](../../Bang/StateMachines/Wait.html#kind) is [WaitKind.Message](../../Bang/StateMachines/WaitKind.html#message). Set by the `ForMessage<T>` overloads to `typeof(T)`; compared against `IMessage` component ids at runtime to know which incoming message satisfies the wait.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
#### EqualityContract
```csharp
protected virtual Type EqualityContract { get; }
```

Compiler-generated member of the `record` type, used internally to make sure `Equals` only ever considers two `Wait`-derived instances equal if they are actually the same runtime type. Not meant to be used directly by game code.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
#### Kind
```csharp
public readonly WaitKind Kind;
```

Which condition the state machine should wait on before resuming this routine. Drives which of [Value](../../Bang/StateMachines/Wait.html#value), [Component](../../Bang/StateMachines/Wait.html#component), [Target](../../Bang/StateMachines/Wait.html#target) and [Routine](../../Bang/StateMachines/Wait.html#routine) are meaningful for this particular instance. See [WaitKind](../../Bang/StateMachines/WaitKind.html) for what each value means.

**Returns** \
[WaitKind](../../Bang/StateMachines/WaitKind.html) \
#### NextFrame
```csharp
public static Wait NextFrame { get; }
```

Wait until the next frame. Equivalent to `ForFrames(0)` — useful to yield control back to the engine for a single tick, e.g. to let a message sent this frame be observed before starting a longer [ForMessage()](../../Bang/StateMachines/Wait.html#formessage) wait.

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \
#### Routine
```csharp
public IEnumerator<T> Routine;
```

Used for [WaitKind.Routine](../../Bang/StateMachines/WaitKind.html#routine). The nested routine created by [ForRoutine(IEnumerator\<T\>)](../../Bang/StateMachines/Wait.html#forroutineienumeratort); the state machine ticks this inner enumerator to completion (as if it were its own current routine) before resuming the routine that yielded this `Wait`, which is what lets one state's routine call into and wait on another as a sub-routine.

**Returns** \
[IEnumerator\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \
#### Stop
```csharp
public readonly static Wait Stop;
```

No longer execute the state machine. `yield return` this (or simply `yield break` at the end of a routine, which has the same effect) to end the state machine for good — once a routine yields `Stop`, `StateMachine.Tick(float)` returns `false` and the owning [StateMachineComponent\<T\>](../../Bang/StateMachines/StateMachineComponent-1.html) is removed from its entity.

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \
#### Target
```csharp
public Entity Target;
```

Used for [WaitKind.Message](../../Bang/StateMachines/WaitKind.html#message) when waiting on another entity that is not the owner of the state machine. When left `null`, the wait listens for the message on the state machine's own owner entity instead.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \
#### Value
```csharp
public T? Value;
```

Integer value, if kind is [WaitKind.Ms](../../Bang/StateMachines/WaitKind.html#ms) or [WaitKind.Frames](../../Bang/StateMachines/WaitKind.html#frames). Also doubles as an optional timeout (in milliseconds) for [WaitKind.Message](../../Bang/StateMachines/WaitKind.html#message) waits created via the `ForMessage<T>(float)`/`ForMessage<T>(Entity, float)` overloads: if the message has not arrived once this many milliseconds pass, the state machine resumes anyway, exactly as if the message had never been waited for.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
### ⭐ Methods
#### PrintMembers(StringBuilder)
```csharp
protected virtual bool PrintMembers(StringBuilder builder)
```

Compiler-generated member of the `record` type, used by the synthesized `ToString()` to print the value of each field. Not meant to be called directly by game code.

**Parameters** \
`builder` [StringBuilder](https://learn.microsoft.com/en-us/dotnet/api/System.Text.StringBuilder?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Wait)
```csharp
public virtual bool Equals(Wait other)
```

Compiler-generated value equality for the `record` type: two `Wait` instances are equal if they have the same [Kind](../../Bang/StateMachines/Wait.html#kind), [Value](../../Bang/StateMachines/Wait.html#value), [Component](../../Bang/StateMachines/Wait.html#component), [Target](../../Bang/StateMachines/Wait.html#target) and [Routine](../../Bang/StateMachines/Wait.html#routine).

**Parameters** \
`other` [Wait](../../Bang/StateMachines/Wait.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Object)
```csharp
public virtual bool Equals(Object obj)
```

Compiler-generated override that forwards to [Equals(Wait)](../../Bang/StateMachines/Wait.html#equalswait) when `obj` is also a `Wait`.

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetHashCode()
```csharp
public virtual int GetHashCode()
```

Compiler-generated hash code combining all of the record's fields, consistent with [Equals(Wait)](../../Bang/StateMachines/Wait.html#equalswait).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ToString()
```csharp
public virtual string ToString()
```

Compiler-generated, debug-friendly string listing the record's field values (via [PrintMembers(StringBuilder)](../../Bang/StateMachines/Wait.html#printmembersstringbuilder)); useful in logs/debugger watches but not meant to be parsed.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ForFrames(int)
```csharp
public Wait ForFrames(int frames)
```

Wait until `frames` engine ticks have occurred before resuming this routine.

**Parameters** \
`frames` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### ForMessage()
```csharp
public Wait ForMessage()
```

Wait until a message of type `T` is sent to the state machine's owner entity, then resume this routine. The message that satisfied the wait can be inspected afterwards via `StateMachine.LastMessage`. There is no timeout — the routine will wait indefinitely unless the message is fired.

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### ForMessage(float)
```csharp
public Wait ForMessage(float maxWait)
```

Wait until message of type `T` is fired no more than `maxWait` seconds. If the message has not been sent by the time `maxWait` elapses, the routine resumes anyway (as if the wait had simply ended), so use `StateMachine.LastMessage` afterwards to tell whether the message actually arrived or the wait timed out.

**Parameters** \
`maxWait` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### ForMessage(Entity)
```csharp
public Wait ForMessage(Entity target)
```

Wait until message of type `T` is fired from `target`, instead of the state machine's own owner entity. Useful for a state machine that needs to react to something happening on another entity, e.g. waiting for the player entity to send a specific message.

**Parameters** \
`target` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### ForMessage(Entity, float)
```csharp
public Wait ForMessage(Entity target, float maxWait)
```

Wait until message of type `T` is fired from `target` no more than `maxWait` seconds. Combines the "listen on another entity" behavior of [ForMessage(Entity)](../../Bang/StateMachines/Wait.html#formessageentity) with the timeout behavior of [ForMessage(float)](../../Bang/StateMachines/Wait.html#formessagefloat).

**Parameters** \
`target` [Entity](../../Bang/Entities/Entity.html) \
`maxWait` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### ForMs(int)
```csharp
public Wait ForMs(int ms)
```

Wait for `ms` milliseconds before resuming this routine.

**Parameters** \
`ms` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### ForRoutine(IEnumerator<T>)
```csharp
public Wait ForRoutine(IEnumerator<T> routine)
```

Wait until `routine` finishes, running it as a nested sub-routine. The state machine ticks `routine` to completion first, then resumes this routine right after the `yield return ForRoutine(...)` line. This is how one state can factor out and call into shared/reusable coroutine logic, similar to calling a sub-function — see `Murder.StateMachines.CoroutineStateMachine`, which exists solely to run an arbitrary `IEnumerator<Wait>` as its one and only state.

**Parameters** \
`routine` [IEnumerator\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \

#### ForSeconds(float)
```csharp
public Wait ForSeconds(float seconds)
```

Wait for `seconds` before resuming this routine. Convenience wrapper over [ForMs(int)](../../Bang/StateMachines/Wait.html#formsint) for the common case of writing wait times in seconds.

**Parameters** \
`seconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Wait](../../Bang/StateMachines/Wait.html) \



⚡

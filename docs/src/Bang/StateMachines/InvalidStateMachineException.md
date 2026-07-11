# InvalidStateMachineException

**Namespace:** Bang.StateMachines \
**Assembly:** Bang.dll

```csharp
public class InvalidStateMachineException : InvalidOperationException
```

Thrown when a [StateMachine](../../Bang/StateMachines/StateMachine.html) (or code that assists one, such as entity/asset lookup helpers) hits a state it cannot recover from on its own — for example a `StateMachine.OnStart` override that depends on a component the entity does not have, or a helper that was asked to fetch a required child entity or asset that does not exist.

Raising this exception, rather than asserting or crashing, lets [StateMachine](../../Bang/StateMachines/StateMachine.html) catch it internally (in `StateMachine.Start` and while ticking) and quietly stop just that one state machine instead of taking down the whole game — see the `catch (InvalidStateMachineException)` blocks in `StateMachine.Start` and `StateMachine.Tick`. Concretely, in `bang\src\Bang\StateMachines\StateMachine.cs`, both the call to `OnStart()` and the call into the active routine are wrapped so that a thrown `InvalidStateMachineException` simply ends that state machine (as if it had `yield return Wait.Stop`) rather than propagating further.

Real call sites throw this when a scripted routine's precondition is not met, for example: `Murder.StateMachines.Dialogs.DialogStateMachine.OnStart` throws when the entity has no `SituationComponent` to talk from; `Murder.Services.EntityServices.FetchRequiredChild` throws when a named child entity a script depends on cannot be found; and `Murder.Services.AssetServices.Create` throws when the requested prefab asset could not be instantiated.

A developer or autonomous agent should throw `InvalidStateMachineException` (instead of a generic exception or an assert) when code running on behalf of a state machine — or setup helpers a state machine's `OnStart`/routine calls into — discovers that required game data or entity state is missing, so the engine can fail that one script gracefully. Outside of state-machine code, prefer a more specific/standard exception type, since only the state-machine tick loop treats this one as recoverable.

**Implements:** _[InvalidOperationException](https://learn.microsoft.com/en-us/dotnet/api/System.InvalidOperationException?view=net-7.0)_

### ⭐ Constructors
```csharp
public InvalidStateMachineException(string message)
```

Creates the exception with a `message` describing what state or data the caller expected to find but did not.

**Parameters** \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — human-readable explanation of what went wrong, for logs/debugging. \

### ⭐ Properties
#### Data
```csharp
public virtual IDictionary Data { get; }
```

Inherited from `Exception`. A free-form key/value bag for attaching extra diagnostic data to the exception; not used by any Bang/Murder code, but available if a caller wants to attach context before the exception is caught and logged.

**Returns** \
[IDictionary](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.IDictionary?view=net-7.0) \
#### HelpLink
```csharp
public string HelpLink { get; set; }
```

Inherited from `Exception`. Optional URL/link to more information about the error; not set by any current throw site in this codebase.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### HResult
```csharp
protected int HResult { get; set; }
```

Inherited from `Exception`. The COM/interop error code associated with this exception; not meaningful for `InvalidStateMachineException`, which is always thrown from managed code.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### InnerException
```csharp
public Exception InnerException { get; }
```

Inherited from `Exception`. The exception that caused this one, if any. `InvalidStateMachineException` is always constructed with just a `message`, so this is `null` for every current throw site in this codebase.

**Returns** \
[Exception](https://learn.microsoft.com/en-us/dotnet/api/System.Exception?view=net-7.0) \
#### Message
```csharp
public virtual string Message { get; }
```

Inherited from `Exception`. The human-readable explanation passed to the constructor — read this in logs/catch blocks to see exactly what precondition failed (e.g. which child entity or component was missing).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Source
```csharp
public virtual string Source { get; set; }
```

Inherited from `Exception`. Name of the application or assembly that raised the exception, as set by the runtime.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### StackTrace
```csharp
public virtual string StackTrace { get; }
```

Inherited from `Exception`. The call stack captured at the point this exception was thrown; the primary tool for tracking down exactly which `StateMachine`/service call raised it.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### TargetSite
```csharp
public MethodBase TargetSite { get; }
```

Inherited from `Exception`. Reflection handle to the method that threw the exception.

**Returns** \
[MethodBase](https://learn.microsoft.com/en-us/dotnet/api/System.Reflection.MethodBase?view=net-7.0) \


⚡

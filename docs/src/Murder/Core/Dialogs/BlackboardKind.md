# BlackboardKind

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed enum BlackboardKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies the scope or category of a blackboard used in the dialogue system.

**Intent:** Distinguishes between the different storage scopes (gameplay-wide, per-character, sound, save-state, etc.) so the engine knows which blackboard store to read from or write to.

**Use-case:** Assign to `IBlackboard.Kind` when implementing a custom blackboard, or read it at runtime to dispatch fact reads/writes to the correct backing store.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### All
```csharp
public static const BlackboardKind All;
```

Targets every blackboard scope simultaneously; used for bulk queries or operations that are not restricted to a single scope.

**Returns** \
[BlackboardKind](../../../Murder/Core/Dialogs/BlackboardKind.html) \
#### Character
```csharp
public static const BlackboardKind Character;
```

Per-character conversation state (e.g. how many times a speaker has been spoken to).

**Returns** \
[BlackboardKind](../../../Murder/Core/Dialogs/BlackboardKind.html) \
#### Gameplay
```csharp
public static const BlackboardKind Gameplay;
```

Global gameplay variables shared across the entire play session (e.g. quest flags, item counts).

**Returns** \
[BlackboardKind](../../../Murder/Core/Dialogs/BlackboardKind.html) \
#### Sound
```csharp
public static const BlackboardKind Sound;
```

Parameters that drive adaptive audio (music and sound FMOD parameters).

**Returns** \
[BlackboardKind](../../../Murder/Core/Dialogs/BlackboardKind.html) \
#### State
```csharp
public static const BlackboardKind State;
```

World or scene state variables that represent persistent environmental conditions.

**Returns** \
[BlackboardKind](../../../Murder/Core/Dialogs/BlackboardKind.html) \


⚡
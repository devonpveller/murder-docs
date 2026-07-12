# BaseCharacterBlackboard

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public class BaseCharacterBlackboard : ICharacterBlackboard
```

Built-in `ICharacterBlackboard` implementation that every character in the dialogue system implicitly gets, tracking state that is not authored by hand in the dialogue editor.

**Intent:** Provides the default per-character blackboard so `CharacterRuntime` always has somewhere to record built-in bookkeeping (currently, total interaction count) without every game needing to declare its own blackboard just for that.

**Use-case:** You normally never instantiate or subclass this directly — the engine registers it automatically via `[Blackboard(Name)]` and `CharacterRuntime` writes to it as a side effect of `NextLine`. Reference `BaseCharacterBlackboard.Name` and `nameof(BaseCharacterBlackboard.TotalInteractions)` in dialogue criteria to gate content on how many times a character has been talked to (e.g. "only show this line the first time we meet").

**Implements:** _[ICharacterBlackboard](../../../Murder/Core/Dialogs/ICharacterBlackboard.html)_

### ⭐ Properties

#### Name

```csharp
public const string Name;
```

The name this blackboard is registered under (`"Character"`). `CharacterRuntime` passes this to `BlackboardTracker.SetInt` when tracking interactions, and dialogue criteria reference it via `Fact.Blackboard` to read `TotalInteractions`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TotalInteractions

```csharp
public int TotalInteractions;
```

Total number of times this character has been interacted with, incremented automatically by `CharacterRuntime` every time a line is advanced via `NextLine`. Do not set this manually unless you specifically intend to reset or seed the counter.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

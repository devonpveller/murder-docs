# Assert

**Namespace:** Bang.Diagnostics \
**Assembly:** Bang.dll

```csharp
public static class Assert
```

Helper class for asserting and throwing exceptions on unexpected scenarios.

Reach for this instead of a normal `if (...) throw new ...` whenever you want to document an invariant inline, at the exact place it must hold, with a single readable call. Unlike [Debug.Assert(bool)](https://learn.microsoft.com/en-us/dotnet/api/System.Diagnostics.Debug.Assert?view=net-7.0), calls here are not stripped from release builds, so they are appropriate for guarding invariants that must never be violated in shipped games (e.g. ECS bookkeeping), not just for debug-time sanity checks.

### ⭐ Methods
#### Verify(bool, string)
```csharp
public static void Verify(bool condition, string text)
```

Verify whether a condition is valid. If not, throw a [InvalidOperationException](https://learn.microsoft.com/en-us/dotnet/api/System.InvalidOperationException?view=net-7.0) with `text` as the message.
            This throws regardless if it's on release on debug binaries.

Use this whenever hitting the failure case means there is a bug in the engine or in game code that should stop execution immediately, rather than being handled gracefully -- for example, invariants about internal Bang state (an entity that must exist, a component that must have been added) where continuing would only corrupt state further and make the eventual failure harder to diagnose. If the failure is instead an expected, recoverable condition (e.g. invalid user input), throw a more specific exception type or handle it explicitly instead of using [Assert.Verify](../../Bang/Diagnostics/Assert.html#verify).

**Parameters** \
`condition` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡
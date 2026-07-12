# ICommands

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public interface ICommands
```

Implemented by static classes that would like to export command functionality.

**Intent:** A marker interface (it declares no members) that `CommandServices` uses to discover which types to scan for debug console commands. During its one-time reflection pass, `CommandServices.FetchAllCommands` enumerates every type in every loaded assembly and keeps only those assignable to `ICommands`, then collects the static methods on those types that carry a [CommandAttribute](../../Murder/Diagnostics/CommandAttribute.html).

**Use-case:** Declare a class that implements `ICommands` and add `[Command("help text")] public static string MyCommand(World world, ...)` methods to it. Because C# does not allow a `static class` to implement an interface, the class itself must be an ordinary (non-static) class, while the individual command methods on it are `static`; what matters to `CommandServices` is only that `typeof(Foo).IsAssignableTo(typeof(ICommands))` and that the methods carry `[Command]` and are `static`. As soon as such a type exists anywhere in a loaded assembly, its `[Command]` methods become callable from the in-game debug console without any further registration step. There are currently no built-in `ICommands` implementors in the engine itself — this is purely an extension point for game projects to plug their own debug commands into `GameLogger`'s console.

⚡

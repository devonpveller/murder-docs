# ListenKeyboardHelper

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class ListenKeyboardHelper : IDisposable
```

A disposable helper that enables raw keyboard text input capture for the duration of its lifetime.

**Intent:** Temporarily enable the keyboard text buffer so you can read typed characters via `PlayerInput.GetKeyboardInput()`.

**Use-case:** Wrap a text-entry UI widget in a `using` statement with `ListenKeyboardHelper` to start capturing keys, then call `PlayerInput.GetKeyboardInput()` each frame to read the typed text. The listener is automatically disabled when the `using` block exits.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors
```csharp
public ListenKeyboardHelper(int maxCharacters)
```

**Parameters** \
`maxCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods
#### Dispose()
```csharp
public virtual void Dispose()
```

#### Clamp(int)
```csharp
public void Clamp(int length)
```

Truncates the captured keyboard text buffer to `length` characters.

**Parameters** \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
# ListenKeyboardHelper

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class ListenKeyboardHelper : IDisposable
```

A disposable helper that enables raw keyboard text input capture for the duration of its lifetime.

**Intent:** Temporarily enable the keyboard text buffer so you can read typed characters via `PlayerInput.GetKeyboardInput()`.

**Use-case:** Wrap a text-entry UI widget's lifetime in a `using` statement/block with `ListenKeyboardHelper` to start capturing keys, then call `PlayerInput.GetKeyboardInput()` (i.e. `Game.Input.GetKeyboardInput()`) each frame to read the typed text. The listener is automatically disabled when the helper is disposed, so it is safe to create and discard one per text field without leaking a persistent keyboard hook. This is only useful for UI/editor style text entry (e.g. renaming an asset, typing a save name); regular gameplay input should use `VirtualButton`/`VirtualAxis` instead.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
public ListenKeyboardHelper(int maxCharacters)
```

Enables `Game.Input`'s raw keyboard text capture (equivalent to `Game.Input.ListenToKeyboardInput(enable: true, maxCharacters)`), clearing any previously buffered text and capping the buffer at `maxCharacters` characters.

**Parameters** \
`maxCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The maximum number of characters the underlying text buffer will accept before further keystrokes are ignored. Defaults to 32 when omitted.

### ⭐ Methods

#### Dispose()

```csharp
public virtual void Dispose()
```

Disables `Game.Input`'s raw keyboard text capture (equivalent to `Game.Input.ListenToKeyboardInput(enable: false)`), unhooking the underlying `TextInputEXT` event so the game stops accumulating typed characters. Call this (or let the `using` block do it) as soon as the text field loses focus.

#### Clamp(int)

```csharp
public static void Clamp(int length)
```

Static convenience wrapper around `Game.Input.ClampText(length)` that truncates the globally buffered keyboard text down to `length` characters. Useful when a text field has a maximum length that is only known after capture has already started (e.g. validating against a dynamic limit), without needing to hold a reference to the `ListenKeyboardHelper` instance.

**Parameters** \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The number of characters to keep from the start of the buffer; any characters beyond this index are discarded.

⚡

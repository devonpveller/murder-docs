# Chord

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed class Chord
```

Represents a keyboard shortcut: one primary key that must be pressed together with zero or more modifier keys (Ctrl/Shift/Alt/Cmd) held down.

**Intent:** Describe a keyboard shortcut that requires one primary key and, optionally, one or more modifier keys held simultaneously.

**Use-case:** Pass a `Chord` to `PlayerInput.Shortcut(Chord)` to detect it being triggered — this is how the editor defines hotkeys such as Ctrl+Z for undo or Ctrl+S for save (see `EditorInputHelpers` and `EditorScene_Shortcuts`). A bare `Keys` value implicitly converts to a modifier-less `Chord`, so most call sites don't need to construct one explicitly.

### ⭐ Constructors

```csharp
public Chord(Keys key, Keys[] modifiers)
```

Creates a chord that triggers when `key` is pressed while every key in `modifiers` is held down.

**Parameters** \
`key` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
Key that must be pressed to trigger this chord. \
`modifiers` [Keys[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
Optional modifiers that need to be pressed along with the key. \

### ⭐ Properties

#### Key

```csharp
public Keys Key { get; }
```

The key that needs to be pressed to trigger this chord.

**Returns** \
[Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

#### Modifiers

```csharp
public Keys[] Modifiers { get; }
```

A list of optional modifiers that need to be pressed along with [Chord.Key](../../../Murder/Core/Input/Chord.html#key) in order to trigger this chord.

**Returns** \
[Keys[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

#### None

```csharp
public static Chord None;
```

A chord bound to `Keys.None` with no modifiers, used as a safe empty/no-op default (e.g. for a shortcut slot that is intentionally unbound).

**Returns** \
[Chord](../../../Murder/Core/Input/Chord.html) \

### ⭐ Methods

#### ToString()

```csharp
public virtual string ToString()
```

Returns a human-readable representation of this chord, joining the modifiers and key with `+` and using friendly names for common modifiers (e.g. `"Shift"`, `"Ctrl"`, `"Cmd"`) — for example `"Ctrl+Z"`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

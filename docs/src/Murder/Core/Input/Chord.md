# Chord

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed class Chord
```

Represents a sequence of Key with optional modifiers.

**Intent:** Describe a keyboard shortcut that requires one primary key and optionally one or more modifier keys held simultaneously.

**Use-case:** Pass a `Chord` to `PlayerInput.Shortcut()` to detect editor hotkeys (e.g. `Ctrl+Z` for undo). Implicitly converts from a single `Keys` value for convenience.

### ⭐ Constructors
```csharp
public Chord(Keys key, Keys[] modifiers)
```

Represents a sequence of Key with optional modifiers.

**Parameters** \
`key` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
\
`modifiers` [Keys[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
\

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

A chord that triggers no key (`Keys.None`), used as a safe empty default.

**Returns** \
[Chord](../../../Murder/Core/Input/Chord.html) \
### ⭐ Methods
#### ToString()
```csharp
public virtual string ToString()
```

Returns a human-readable representation of this chord (e.g. `"Ctrl+Z"`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡
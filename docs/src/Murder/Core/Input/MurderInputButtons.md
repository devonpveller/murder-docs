# MurderInputButtons

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class MurderInputButtons
```

Base class for input button constants, numbers from 100 to 120 are reserved for the engine.
            We recomend that if you need to create new constants for more gameplay buttons, start at 0.

**Intent:** Defines the built-in logical input button action IDs reserved by the engine.

**Use-case:** Refer to these constants when registering physical input bindings with `PlayerInput`; reserve IDs below 100 for game-specific buttons.

### ⭐ Constructors
```csharp
public MurderInputButtons()
```

### ⭐ Properties
#### Cancel
```csharp
public static const int Cancel;
```

Button ID for the cancel/back action.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Ctrl
```csharp
public static const int Ctrl;
```

Button ID for the Ctrl modifier key.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Debug
```csharp
public static const int Debug;
```

Button ID used for debug-mode actions.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Delete
```csharp
public static const int Delete;
```

Button ID for the Delete key.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Esc
```csharp
public static const int Esc;
```

Button ID for the Escape key.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### LeftClick
```csharp
public static const int LeftClick;
```

Button ID for the left mouse button.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### MiddleClick
```csharp
public static const int MiddleClick;
```

Button ID for the middle mouse button.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Pause
```csharp
public static const int Pause;
```

Button ID for the pause action.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### PlayGame
```csharp
public static const int PlayGame;
```

Button ID for starting or resuming gameplay.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### RightClick
```csharp
public static const int RightClick;
```

Button ID for the right mouse button.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Shift
```csharp
public static const int Shift;
```

Button ID for the Shift modifier key.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Space
```csharp
public static const int Space;
```

Button ID for the Spacebar / Backspace key.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Submit
```csharp
public static const int Submit;
```

Button ID for the confirm/submit action (e.g. Enter, A button).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
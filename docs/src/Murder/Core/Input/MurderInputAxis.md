# MurderInputAxis

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class MurderInputAxis
```

Base class for input axis constants, numbers from 100 to 120 are reserved for the engine.
            We recomend that if you need to create new constants for more gameplay axis, start at 0.

**Intent:** Defines the built-in logical input axis action IDs reserved by the engine.

**Use-case:** Refer to these constants when registering physical input bindings with `PlayerInput`; reserve IDs below 100 for game-specific axes.

### ⭐ Constructors
```csharp
public MurderInputAxis()
```

### ⭐ Properties
#### EditorCamera
```csharp
public static const int EditorCamera;
```

Axis ID for panning the editor camera.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Movement
```csharp
public static const int Movement;
```

Axis ID for entity/player movement.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Ui
```csharp
public static const int Ui;
```

Axis ID for navigating menu/UI elements.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### UiTab
```csharp
public static const int UiTab;
```

Axis ID for switching between tabs in a tabbed UI panel.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡
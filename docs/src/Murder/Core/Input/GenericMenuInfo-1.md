# GenericMenuInfo\<T\>

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct GenericMenuInfo<T>
```

State container for a typed menu with keyboard/gamepad navigation — tracks selection, scroll, overflow, and cancel state.

**Intent:** Drive strongly-typed menu navigation with `PlayerInput.VerticalMenu<T>()`.

**Use-case:** Declare a `GenericMenuInfo<MyOption>` field in your UI state. Pass it by reference to `PlayerInput.VerticalMenu<T>()` or `GridMenu<T>()` each frame to receive selection updates and pressed/canceled flags.

### ⭐ Constructors
```csharp
public GenericMenuInfo<T>(T[] options)
```

**Parameters** \
`options` [T[]](../../../) \

### ⭐ Properties
#### Canceled
```csharp
public bool Canceled;
```

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Disabled
```csharp
public bool Disabled;
```

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### JustMoved
```csharp
public bool JustMoved;
```

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### LastMoved
```csharp
public float LastMoved;
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### LastPressed
```csharp
public float LastPressed;
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Length
```csharp
public int Length { get; }
```

Number of options in this menu

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Options
```csharp
public T[] Options;
```

The array of options available in this menu.

**Returns** \
[T[]](../../../) \
#### Overflow
```csharp
public int Overflow;
```

Direction the cursor tried to move beyond the menu's bounds (−1, 0, or +1).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### PreviousSelection
```csharp
public int PreviousSelection;
```

The index that was selected before the most recent navigation.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Scroll
```csharp
public int Scroll;
```

The index of the first visible option when the list is taller than `VisibleItems`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Selection
```csharp
public int Selection { get; private set; }
```

The currently highlighted option index.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Sounds
```csharp
public MenuSounds Sounds;
```

Sound events played on selection change, submit, and cancel.

**Returns** \
[MenuSounds](../../../Murder/Core/Sounds/MenuSounds.html) \
#### VisibleItems
```csharp
public int VisibleItems;
```

Number of visible options on the screen, 8 is the default.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### NextAvailableOption(int, int)
```csharp
public int NextAvailableOption(int option, int direction)
```

Returns the next selectable option index starting from `option` and moving in `direction` (+1 or −1), wrapping around.

**Parameters** \
`option` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\
`direction` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

#### Select(int, float)
```csharp
public void Select(int index, float now)
```

Moves the selection to `index`, plays the selection-change sound if the index changed, and records the move timestamp.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`now` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Select(int)
```csharp
public void Select(int index)
```

Moves the selection to `index`.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
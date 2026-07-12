# GenericMenuInfo\<T\>

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public struct GenericMenuInfo<T>
```

Strongly-typed state container for keyboard/gamepad menu navigation over an array of `T` options.

**Intent:** Let game code react to menu selection by indexing back into a real, typed array of option values (e.g. inventory items, save slots, settings enum values) rather than just a display string, unlike `MenuInfo` which stores pre-formatted option strings for immediate-mode UI.

**Use-case:** Declare a `GenericMenuInfo<MyOption>` field in your UI state, kept by the caller (typically a UI component or system). Pass it by reference each frame to `PlayerInput.VerticalMenu<T>(ref GenericMenuInfo<T>)` or `PlayerInput.GridMenu<T>(ref GenericMenuInfo<T>, int, int, GridMenuFlags)` to receive selection updates and pressed/canceled flags.

### ⭐ Constructors

```csharp
public GenericMenuInfo<T>(T[] options)
```

Creates a menu over the given set of options, starting with no explicit selection (index 0 is selected by default since `Selection` defaults to 0).

**Parameters** \
`options` [T[]](../../../) \
The full set of selectable options this menu will navigate. \

### ⭐ Properties

#### Canceled

```csharp
public bool Canceled;
```

Set to `true` for the frame the player triggered the menu's cancel/back action.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Disabled

```csharp
public bool Disabled;
```

When `true`, input navigation and selection are ignored for this menu.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### JustMoved

```csharp
public bool JustMoved;
```

Set to `true` for the frame in which `Selection` changed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LastMoved

```csharp
public float LastMoved;
```

The `Game.NowUnscaled` timestamp of the last time `Selection` changed, via `Select(int, float)`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LastPressed

```csharp
public float LastPressed;
```

The `Game.NowUnscaled` timestamp of the last time the submit action was pressed on this menu.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Length

```csharp
public int Length { get; }
```

Number of options in this menu.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Options

```csharp
public T[] Options;
```

The array of options available in this menu. Indexed by `Selection` to retrieve the currently highlighted value.

**Returns** \
[T[]](../../../) \

#### OverflowX

```csharp
public int OverflowX;
```

Direction (-1, 0, or +1) the cursor tried to move past the horizontal bounds of the menu on the last navigation attempt; used by grid menus.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### OverflowY

```csharp
public int OverflowY;
```

Direction (-1, 0, or +1) the cursor tried to move past the vertical bounds of the menu on the last navigation attempt; used by grid menus.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### PreviousSelection

```csharp
public int PreviousSelection;
```

The index that was selected immediately before the most recent call to `Select(int, float)`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Scroll

```csharp
public int Scroll;
```

The index of the first visible option when the list is taller than `VisibleItems`, used to keep the selection scrolled into view.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Selection

```csharp
public int Selection { get; private set; }
```

The index of the currently highlighted option in `Options`. Change it through `Select(int, float)` rather than assigning directly, so scroll/sound/timing state stays consistent.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SmoothScroll

```csharp
public float SmoothScroll;
```

An interpolated (eased) version of `Scroll` intended for smooth-scrolling UI rendering; not used for input logic itself.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Sounds

```csharp
public MenuSounds Sounds;
```

Sound events played on selection change, submit, and cancel for this menu instance.

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

Computes the option index reached by moving one step from `option` in `direction`, wrapping around the ends of `Options`. Used internally by `PlayerInput`'s menu-advancing methods to resolve arrow-key/D-pad navigation.

**Parameters** \
`option` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The currently selected option. If -1, it means that is being initialized. \
`direction` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
A sign number (1 or -1) with the direction. \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The next option that is available. \

#### Select(int, float)

```csharp
public void Select(int index, float now)
```

Moves the selection to `index`, recording `PreviousSelection` and `LastMoved`, and playing `MenuSounds.SelectionChange` if the selection actually changed. This is the method `PlayerInput`'s menu-advancing calls use to commit a navigation step; prefer it over assigning `Selection` directly.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The option index to select. \
`now` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
The current time (typically `Game.NowUnscaled`) to stamp `LastMoved` with. \

⚡

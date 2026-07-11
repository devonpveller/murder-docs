# MenuInfo

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct MenuInfo
```

State container for a `MenuOption`-based menu with keyboard/gamepad navigation, scroll, and per-option availability.

**Intent:** Drive a simple navigable menu backed by `MenuOption` entries.

**Use-case:** Declare a `MenuInfo` and pass it by reference to `PlayerInput.VerticalMenu()` or `HorizontalMenu()` each frame. Read `Selection` for the highlighted index and check the return value for a confirmed press.

### ⭐ Constructors
```csharp
public MenuInfo()
```

```csharp
public MenuInfo(MenuOption[] options)
```

**Parameters** \
`options` [MenuOption[]](../../../Murder/Services/MenuOption.html) \

```csharp
public MenuInfo(IEnumerable<T> options)
```

**Parameters** \
`options` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

```csharp
public MenuInfo(int size)
```

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public MenuInfo(String[] options)
```

**Parameters** \
`options` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Canceled
```csharp
public bool Canceled;
```

Set to `true` this frame if the cancel button was pressed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Disabled
```csharp
public bool Disabled;
```

When `true`, navigation input is ignored and the menu will not move.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### HasOptions
```csharp
public bool HasOptions { get; }
```

Returns `true` if `Options` is non-null and non-empty.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Icons
```csharp
public Portrait[] Icons;
```

Optional icons to be displayed near the options.

**Returns** \
[Portrait[]](../../../Murder/Core/Portrait.html) \
#### JustMoved
```csharp
public bool JustMoved;
```

`true` for the frame when the selection index changed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### LargestOptionText
```csharp
public float LargestOptionText { get; }
```

The pixel width of the widest option text label, used for sizing the menu container.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### LastMoved
```csharp
public float LastMoved;
```

Timestamp (unscaled time) of the most recent selection change.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### LastPressed
```csharp
public float LastPressed;
```

Timestamp (unscaled time) of the most recent submit press.

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
public MenuOption[] Options;
```

The array of selectable options in this menu.

**Returns** \
[MenuOption[]](../../../Murder/Services/MenuOption.html) \
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
#### IsOptionAvailable(int)
```csharp
public bool IsOptionAvailable(int option)
```

Returns `true` if the option at `option` is currently selectable.

**Parameters** \
`option` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### NextAvailableOption(int, int)
```csharp
public int NextAvailableOption(int option, int direction)
```

Returns the next selectable option index starting from `option` moving in `direction`.

**Parameters** \
`option` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\
`direction` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

#### Disable(bool)
```csharp
public MenuInfo Disable(bool disabled)
```

Returns a copy of this `MenuInfo` with `Disabled` set to `disabled`.

**Parameters** \
`disabled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[MenuInfo](../../../Murder/Core/Input/MenuInfo.html) \

#### GetOptionText(int)
```csharp
public string GetOptionText(int index)
```

Returns the display text for the option at `index`.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSelectedOptionText()
```csharp
public string GetSelectedOptionText()
```

Returns the display text for the currently selected option.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Cancel()
```csharp
public void Cancel()
```

Marks this menu as canceled.

#### Clamp(int)
```csharp
public void Clamp(int max)
```

Clamps `Selection` to be within [0, `max`-1].

**Parameters** \
`max` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Press(float)
```csharp
public void Press(float now)
```

Records a submit press at time `now`.

**Parameters** \
`now` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Reset()
```csharp
public void Reset()
```

Resets the menu info selector to the first available option.

#### Resize(int)
```csharp
public void Resize(int size)
```

Resizes the options array to `size`.

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Select(int, float)
```csharp
public void Select(int index, float now)
```

Moves selection to `index` and records the timestamp `now`.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`now` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Select(int)
```csharp
public void Select(int index)
```

Moves selection to `index`.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SnapLeft(int)
```csharp
public void SnapLeft(int width)
```

Snaps the selection to the leftmost column in a grid menu of `width` columns.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SnapRight(int)
```csharp
public void SnapRight(int width)
```

Snaps the selection to the rightmost column in a grid menu of `width` columns.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
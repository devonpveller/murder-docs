# MenuOption

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public sealed struct MenuOption
```

Represents a single selectable item in a rendered vertical menu.

**Intent:** Holds the display text and interaction state for one row in a menu drawn by `RenderServices.DrawVerticalMenu`.

**Use-case:** Build an array of `MenuOption` values and pass it inside a `MenuInfo` to the draw helpers to render an interactive menu list with correct enabled/faded/sound states.

### ⭐ Constructors
```csharp
public MenuOption()
```

```csharp
public MenuOption(bool selectable)
```

**Parameters** \
`selectable` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public MenuOption(string text, bool selectable)
```

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`selectable` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### Enabled
```csharp
public bool Enabled { get; public set; }
```
When `true`, the item can be selected by the player; `false` renders it as disabled.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Faded
```csharp
public bool Faded { get; public set; }
```
When `true`, the item is drawn at reduced opacity to indicate it is inactive or unavailable.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Length
```csharp
public int Length { get; }
```

Length of the text option.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### SoundOnClick
```csharp
public bool SoundOnClick;
```
When `true`, a click sound is played when this item is selected.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Text
```csharp
public readonly string Text;
```
The display label shown for this menu item.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡
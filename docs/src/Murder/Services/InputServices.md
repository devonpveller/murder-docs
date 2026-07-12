# InputServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class InputServices
```

Helpers for building the player-facing "rebind your controls" menu and for safely parsing numeric strings from input-related data.

**Intent:** Bridges the `InputGraphicsAsset`/`InputProfileAsset` configuration (authored in the editor) and the live `Game.Input` button/axis registry into a ready-to-render [GenericMenuInfo&lt;InputMenuOption&gt;](../../Murder/Core/Input/GenericMenuInfo-1.html), so a settings screen doesn't need to know how buttons/axes are represented internally.

**Use-case:** Call `CreateBindingsMenuInfo` when building a controls/rebinding settings screen, to get one `InputMenuOption` per customizable button/axis (plus optional "swap submit/cancel", "allow mouse clicks", "reset to default", and "exit" entries). Use `GetButtonInfo` to look up a button's configured `InputInformation` (e.g. to render its current binding) by id. Use `ParseFloatSafe`/`ParseIntSafe` when reading numeric values out of input configuration or profile strings that might be malformed, without needing a try/catch at every call site.

### ⭐ Methods

#### CreateBindingsMenuInfo(string, string, string, string)

```csharp
public static GenericMenuInfo<InputMenuOption> CreateBindingsMenuInfo(string? reset, string? exitText, string? swapSubmit, string? allowMouse)
```

Builds the full list of rebindable-control menu entries from the active `InputGraphicsAsset`/`InputProfileAsset` (resolved from `Game.Profile`): one `InputMenuOption` per button/axis flagged `AllowPlayerCustomization`, plus optional trailing entries controlled by the nullable parameters — a "swap submit/cancel" toggle (`swapSubmit`), an "allow mouse clicks" toggle (`allowMouse`), a "reset all bindings" entry (`reset`), and an "exit" entry (`exitText`), each included only if its corresponding text is non-`null`. Logs an error and returns an empty `GenericMenuInfo` if the game profile's input graphics or input profile asset isn't configured. Analogue-axis binding entries are currently commented out in source ("since we don't allow customization") — only digital-press axis entries are added.

**Parameters** \
`reset` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`exitText` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`swapSubmit` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`allowMouse` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GenericMenuInfo\<InputMenuOption\>](../../Murder/Core/Input/GenericMenuInfo-1.html) \

#### GetButtonInfo(int)

```csharp
public static InputInformation? GetButtonInfo(int id)
```

Looks up the `InputInformation` entry for the button `id` in the active `InputProfileAsset`. Returns `null` if the game profile has no input profile asset configured, or if no button with that id is found. Note the source flags this lookup as something that "should be cached" — it does a linear scan over every button on each call.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[InputInformation?](../../Murder/Assets/Input/InputInformation.html) \

#### ParseFloatSafe(string)

```csharp
public static float ParseFloatSafe(string s)
```

Parses `s` as a `float` using the invariant culture; if parsing fails, logs the error and returns `1` instead of throwing. Use this when reading a numeric value from data that might be malformed and a sane fallback is preferable to crashing.

**Parameters** \
`s` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ParseIntSafe(string, NumberStyles)

```csharp
public static int ParseIntSafe(string s, NumberStyles style = NumberStyles.Integer)
```

Parses `s` as an `int` using the invariant culture and the given `NumberStyles`; if parsing fails, logs the error and returns `1` instead of throwing.

**Parameters** \
`s` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`style` [NumberStyles](https://learn.microsoft.com/en-us/dotnet/api/System.Globalization.NumberStyles?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

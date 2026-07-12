# MenuInfo

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public struct MenuInfo
```

State container for an untyped, `MenuOption`-based menu with keyboard/gamepad navigation, scrolling, per-option availability and sound feedback. This is the non-generic sibling of `GenericMenuInfo<T>`; unlike the generic version its `Options` array carries display text and an `Enabled` flag per entry (via `MenuOption`), and it additionally tracks scroll-smoothing, timestamps, icons and a submit "attempt" counter used by UI code to animate a disabled selection being pressed.

**Intent:** Drive a simple navigable menu backed by `MenuOption` entries without hand-rolling selection/scroll/sound bookkeeping in every screen.

**Use-case:** Declare a `MenuInfo` field (often via one of its `string[]`/`MenuOption[]` constructors) and pass it by `ref` to `PlayerInput.VerticalMenu(ref MenuInfo, ...)`, `HorizontalMenu(ref MenuInfo, ...)` or `GridMenu(ref MenuInfo, ...)` once per frame. Read `Selection`/`GetSelectedOptionText()` for the highlighted option, `JustMoved` to detect a change this frame, and check the boolean returned by the `PlayerInput` call (or `Canceled`) to know whether the player confirmed or backed out.

### ⭐ Constructors

```csharp
public MenuInfo()
```

Creates an empty menu with no options, stamping `CreatedAt`/`LastMoved` with the current unscaled time. Use one of the overloads below (or `Resize`) to populate `Options` afterwards.

```csharp
public MenuInfo(MenuOption[] options)
```

Creates a menu from an explicit array of `MenuOption` entries (each carrying its own text and `Enabled` flag). If the first option isn't enabled, the initial `Selection` is advanced to the next available option automatically.

**Parameters** \
`options` [MenuOption[]](../../../Murder/Services/MenuOption.html) \

```csharp
public MenuInfo(IEnumerable<MenuOption> options)
```

Convenience overload that materializes `options` into an array and forwards to the `MenuOption[]` constructor.

**Parameters** \
`options` [IEnumerable\<MenuOption\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

```csharp
public MenuInfo(IEnumerable<MenuOption> options, int startSelectedAt)
```

Same as `MenuInfo(IEnumerable<MenuOption>)`, but also seeds `Selection` (and `PreviousSelection`) at `startSelectedAt` instead of the default first available option — useful when reopening a menu and wanting to resume at the previously chosen entry.

**Parameters** \
`options` [IEnumerable\<MenuOption\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
`startSelectedAt` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public MenuInfo(string[] options)
```

Builds `Options` from an array of plain strings, wrapping each one in a `MenuOption` that is enabled and plays a click sound by default. This is the simplest way to spin up a menu when you just need labeled, always-selectable entries.

**Parameters** \
`options` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

```csharp
public MenuInfo(IEnumerable<string> options)
```

Convenience overload of the `string[]` constructor for any `IEnumerable<string>` source (e.g. a `List<string>` or LINQ query result).

**Parameters** \
`options` [IEnumerable\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

```csharp
public MenuInfo(int size)
```

Allocates `size` enabled, empty-text `MenuOption` slots via `Resize(size)` — useful when the option count is known up front but the labels/icons are filled in later (e.g. bound to a dynamic list of inventory items).

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public MenuInfo(int size, int startSelectedAt)
```

Same as `MenuInfo(int)`, but also seeds `Selection`/`PreviousSelection` at `startSelectedAt`.

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`startSelectedAt` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### AcceptPressInputFeedback

```csharp
public bool AcceptPressInputFeedback;
```

When `true` (the default), calling `Press(float)` plays `Sounds.MenuSubmit` and bumps `AttemptedPressCurrentSelection`/`LastPressed`; when `false`, `Press` becomes a no-op. `PlayerInput.HorizontalMenu`/`VerticalMenu` also gate whether the submit button gets consumed on this flag, so setting it to `false` lets you show a menu that visually reacts to the cursor but ignores confirm presses (e.g. while a modal is animating in).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AttemptedPressCurrentSelection

```csharp
public int AttemptedPressCurrentSelection;
```

Counts how many times `Press` has been called against the current `Selection` since it last changed. Reset to zero every time `Select` runs. UI code can use this to, for example, shake a disabled option or play an escalating "denied" animation if the player keeps mashing submit on it.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Canceled

```csharp
public bool Canceled;
```

Set to `true` for the frame the cancel button (`MurderInputButtons.Cancel`) was pressed while this menu was being updated by `PlayerInput`. Check this after calling `VerticalMenu`/`HorizontalMenu`/`GridMenu` to know the player backed out instead of confirming.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CapacityToShowUi

```csharp
public int CapacityToShowUi;
```

The allowed number of options visible in the view, used by rendering code to size UI elements on screen (defaults to 8). Distinct from `VisibleItems`, which drives the scroll math in `PlayerInput`; this one is purely a layout hint for the presentation layer.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### CreatedAt

```csharp
public float CreatedAt;
```

Unscaled timestamp (from `Game.NowUnscaled`) captured when this `MenuInfo` was constructed. Useful for driving one-shot "menu just opened" entrance animations relative to a stable origin time.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Disabled

```csharp
public bool Disabled;
```

When `true`, `PlayerInput.HorizontalMenu`/`VerticalMenu`/`GridMenu` skip all input handling for this menu entirely (no selection change, no submit, no cancel) and return `false`. Use this to freeze a menu in place while another UI element has focus, without losing its current selection state.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasAvailableOptions

```csharp
public bool HasAvailableOptions { get; }
```

Returns `true` if `HasOptions` is `true` and at least one entry in `Options` has `Enabled` set. Use this to decide whether a menu is worth showing/navigable at all, as opposed to `HasOptions`, which only checks that the array isn't empty.

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

Optional per-option icons to be displayed alongside the text in `Options`, indexed in parallel with it. Left empty (`[]`) by default; populate it manually when a menu needs to show item/character portraits next to each entry.

**Returns** \
[Portrait[]](../../../Murder/Core/Portrait.html) \

#### JustMoved

```csharp
public bool JustMoved;
```

`true` for the single frame the selection index actually changed. `PlayerInput.HorizontalMenu`/`VerticalMenu` reset this to `false` at the start of every update before recomputing it, so it should only be read after calling one of those methods for the current frame — useful for triggering a "move" sound/animation exactly once per navigation.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LargestOptionText

```csharp
public float LargestOptionText { get; }
```

The pixel width (via `MurderFonts.PixelFont`) of the widest option's text label, recomputed on every access. Used for sizing the menu's background/container to fit its longest entry.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LastMoved

```csharp
public float LastMoved;
```

Unscaled timestamp of the most recent navigation input, updated on every `Select` call and by `PlayerInput`'s menu helpers even when the selection didn't actually change (e.g. movement was attempted but clamped). Distinct from `LastMovedSucessfully`, which only updates when the selection index genuinely changed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LastMovedSucessfully

```csharp
public float LastMovedSucessfully;
```

Unscaled timestamp of the most recent frame the selection actually changed (`JustMoved` was `true`). Use this instead of `LastMoved` when you need to know "how long has the current selection been stable" for animation easing.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LastPressed

```csharp
public float LastPressed;
```

Unscaled timestamp of the most recent submit press (updated by both `Select` and `Press`). Useful for animating a "just confirmed" flash on the selected option.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Length

```csharp
public int Length { get; }
```

Number of options in this menu; returns `0` when `HasOptions` is `false` rather than throwing on a null `Options` array.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Options

```csharp
public MenuOption[] Options;
```

The array of selectable options in this menu, each with its own text, `Enabled` flag and click-sound behaviour. Populated by the constructors, `Resize`, or assigned directly.

**Returns** \
[MenuOption[]](../../../Murder/Services/MenuOption.html) \

#### OverflowX

```csharp
public int OverflowX;
```

Set by `PlayerInput`'s menu helpers to `-1`/`0`/`1` indicating the horizontal direction the player tried to move the cursor beyond the menu's bounds this frame (e.g. pressing right in a `VerticalMenu`, which has no horizontal axis of its own). UI code can use this to, for example, shift focus to an adjacent panel.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### OverflowY

```csharp
public int OverflowY;
```

Same as `OverflowX` but for vertical overflow (e.g. pressing up/down in a `HorizontalMenu`, or past the top/bottom row of a `GridMenu` with clamping flags set).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### PreviousSelection

```csharp
public int PreviousSelection;
```

The index that was selected immediately before the most recent `Select` call. Useful for detecting the direction of movement (`Selection - PreviousSelection`) or for playing a transition animation between the old and new highlighted option.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Scroll

```csharp
public int Scroll;
```

The index of the first visible option when the list is taller than `VisibleItems`. Updated automatically by `Select` (and by `PlayerInput`'s grid helper) to keep the current `Selection` within the visible window.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Selection

```csharp
public int Selection { get; private set; }
```

The currently highlighted option index. Read-only from outside the struct — change it via `Select(int)`/`Select(int, float, bool)` (or indirectly through `PlayerInput`'s menu helpers) rather than assigning it directly, since those methods also update `JustMoved`, `Scroll`, timestamps and play the selection-change sound.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SmoothScroll

```csharp
public float SmoothScroll;
```

An eased (lerp-smoothed) version of `Scroll`, recomputed every frame by `PlayerInput`'s menu helpers via `Calculator.LerpSmooth`. Rendering code should use this instead of the integer `Scroll` when animating the list's scroll offset, so it glides rather than snaps.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Sounds

```csharp
public MenuSounds Sounds;
```

Sound events played on selection change (`SelectionChange`) and submit (`MenuSubmit`). Assign a custom `MenuSounds` value to override the default cues for a specific menu instance.

**Returns** \
[MenuSounds](../../../Murder/Core/Sounds/MenuSounds.html) \

#### VisibleItems

```csharp
public int VisibleItems;
```

Number of options visible on screen at once; 8 is the default. `Select` and `PlayerInput`'s grid helper use this to decide when to advance `Scroll` so the current selection stays within the visible window.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### IsOptionAvailable(int)

```csharp
public bool IsOptionAvailable(int option)
```

Returns `true` if the option at `option` is currently selectable — `true` when `Options` is `null` (nothing to disqualify it), `false` if `option` is out of range, otherwise the entry's `Enabled` flag. Used internally by `NextAvailableOption` and the grid-navigation helpers to skip disabled entries while moving the cursor.

**Parameters** \
`option` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### NextAvailableOption(int, int, GridMenuFlags)

```csharp
public int NextAvailableOption(int option, int direction, GridMenuFlags flags)
```

Walks from `option` in `direction` (`+1`/`-1`), wrapping around the ends of `Options`, until it finds an index for which `IsOptionAvailable` is `true`, and returns it. When `flags` includes `ClampLeft`/`ClampRight`, movement stops at the boundary instead of wrapping. This is what `PlayerInput.HorizontalMenu`/`VerticalMenu` call every frame to translate a raw axis tick into the next selectable option, skipping over any disabled entries along the way.

**Parameters** \
`option` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The currently selected option to search from. \
`direction` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
A sign number (`1` or `-1`) indicating the search direction. \
`flags` [GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \
Clamp options; defaults to `GridMenuFlags.None` (wrap around).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The next option that is available.

#### NextAvailableOptionHorizontal(int, int, int, GridMenuFlags)

```csharp
public (int option, bool wrapped) NextAvailableOptionHorizontal(int option, int width, int direction, GridMenuFlags flags)
```

Grid-aware horizontal search: starting from `option` in a grid of `width` columns, looks for the next available option in the same row moving in `direction`, honoring `ClampLeft`/`ClampRight`; if the row has no more candidates it falls back to scanning nearby rows for a match in the target column. Returns the found index together with whether the search wrapped around a clamped edge. Called by `PlayerInput.GridMenu(ref MenuInfo, ...)` to resolve horizontal cursor movement; not something game code typically needs to call directly.

**Parameters** \
`option` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`direction` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`flags` [GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

**Returns** \
[(int, bool)](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \
The resolved option index and whether the movement wrapped around a clamped edge.

#### NextAvailableOptionVertical(int, int, int, GridMenuFlags)

```csharp
public (int option, bool wrapped) NextAvailableOptionVertical(int option, int width, int direction, GridMenuFlags flags)
```

Grid-aware vertical counterpart to `NextAvailableOptionHorizontal`: searches rows above/below `option` (grid of `width` columns) for the next available option in the same column, honoring `ClampTop`/`ClampBottom`, then falls back to nearby columns, and finally to `NextAvailableOptionHorizontal` if nothing is found. Called by `PlayerInput.GridMenu(ref MenuInfo, ...)` to resolve vertical cursor movement.

**Parameters** \
`option` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`direction` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`flags` [GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

**Returns** \
[(int, bool)](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \
The resolved option index and whether the movement wrapped around a clamped edge.

#### Disable(bool)

```csharp
public MenuInfo Disable(bool disabled)
```

Sets `Disabled` and returns `this`, so a fresh or existing `MenuInfo` can be configured fluently inline, e.g. `var menu = new MenuInfo(options).Disable(true);`.

**Parameters** \
`disabled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[MenuInfo](../../../Murder/Core/Input/MenuInfo.html) \

#### GetOptionText(int)

```csharp
public string GetOptionText(int index)
```

Returns the display text for the option at `index`, wrapping via modulo (`index % Options.Length`) so an out-of-range index still resolves to a valid entry instead of throwing.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSelectedOptionText()

```csharp
public string GetSelectedOptionText()
```

Returns the display text for the currently selected option (`Options[Selection].Text`) — the most common way UI code reads what's highlighted without indexing `Options` manually.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Cancel()

```csharp
public void Cancel()
```

Hook called by `PlayerInput` when the cancel button is pressed for this menu. Currently a no-op body (the cancel sound playback is commented out in source) — `Canceled` is what actually gets set to `true` by the caller; override/extend this only if you need to observe cancellation via a different mechanism.

#### Clamp()

```csharp
public void Clamp()
```

If `Selection` is out of range or currently points at a disabled option, advances it to the next available option (via `NextAvailableOption`). Call this after mutating `Options` externally (e.g. disabling an entry) to make sure the selection doesn't end up stuck on an invalid or disabled index.

#### Press(float)

```csharp
public void Press(float now)
```

Records a submit press at time `now`: increments `AttemptedPressCurrentSelection`, updates `LastPressed`, and — when `AcceptPressInputFeedback` is `true` and the selected option has `SoundOnClick` set — plays `Sounds.MenuSubmit`. Called by `PlayerInput`'s menu helpers when the submit button is pressed; rarely needs to be called directly by game code.

**Parameters** \
`now` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Reset()

```csharp
public void Reset()
```

Resets `Selection` to `0`, stamps `LastMoved`/`LastMovedSucessfully` with the current unscaled time, and sets `PreviousSelection` to `-1`. Use this when reopening/reinitializing a menu (e.g. a pause menu each time it's shown) so it doesn't remember a stale selection from last time.

#### Resize(int)

```csharp
public void Resize(int size)
```

Reallocates `Options` to `size` new, enabled, empty-text `MenuOption` entries, discarding any previous content. If the current `Selection` pointed at the old last index, it's re-clamped to the new last index. Use this to change how many options a menu has at runtime (e.g. a dynamically-sized inventory list) instead of constructing a whole new `MenuInfo`.

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Select(int)

```csharp
public void Select(int index)
```

Shorthand for `Select(index, Game.NowUnscaled, true)` — moves the selection to `index` using the current time and default scroll behavior.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Select(int, float, bool)

```csharp
public void Select(int index, float now, bool updateScroll)
```

The core selection-mutation method: moves `Selection` to `index` (clamped to `Options` bounds), records `PreviousSelection`, updates `JustMoved`/`LastMoved`/`LastPressed`/`LastMovedSucessfully`, resets `AttemptedPressCurrentSelection`, and — if the move changed the selection and the new option is enabled — plays `Sounds.SelectionChange`. When `updateScroll` is `true` (the default via the 2-arg `Select`), also adjusts `Scroll` so `index` stays within the `VisibleItems` window. `PlayerInput`'s menu helpers call this every frame a navigation input is detected; call it yourself to force a specific selection (e.g. jumping to an option the player clicked with the mouse).

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`now` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`updateScroll` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether to also update `Scroll` to keep `index` visible; defaults to `true`.

#### SnapLeft(int)

```csharp
public void SnapLeft(int width)
```

Snaps `Selection` to the leftmost column of its current row in a grid menu of `width` columns.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SnapRight(int)

```csharp
public void SnapRight(int width)
```

Snaps `Selection` to the rightmost column of its current row in a grid menu of `width` columns.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡

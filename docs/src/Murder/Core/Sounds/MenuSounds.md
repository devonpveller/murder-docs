# MenuSounds

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct MenuSounds
```

A small bundle of `SoundEventId` references for the sound effects a menu widget plays as the player navigates it: confirming, cancelling, changing the highlighted item, switching tabs, and hitting an error/invalid action. Every field defaults to an empty (unassigned) `SoundEventId`, so a menu that doesn't set `Sounds` simply stays silent instead of throwing.

**Intent:** Provide a convenient, single bundle of UI sound events that a menu widget can carry around instead of five separate fields.

**Use-case:** `MenuInfo`/`GenericMenuInfo<T>` expose a public `Sounds` field of this type; assign it once (typically from the editor) and the menu widget's own update logic calls `SoundServices.Play(Sounds.SelectionChange)`, `SoundServices.Play(Sounds.MenuSubmit)`, etc. at the right moments so navigation, submission, and cancellation all play the appropriate sounds automatically without the menu code needing to know which specific FMOD events are involved.

### ⭐ Properties

#### Cancel

```csharp
public readonly SoundEventId Cancel { get; init; }
```

Sound event played when the player cancels or backs out of a menu.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

#### MenuSubmit

```csharp
public readonly SoundEventId MenuSubmit { get; init; }
```

Sound event played when the player confirms a menu selection.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

#### OnError

```csharp
public readonly SoundEventId OnError { get; init; }
```

Sound event played when the player attempts an invalid or unavailable action.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

#### SelectionChange

```csharp
public readonly SoundEventId SelectionChange { get; init; }
```

Sound event played each time the highlighted menu item changes.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

#### TabSwitchChange

```csharp
public readonly SoundEventId TabSwitchChange { get; init; }
```

Sound event played when switching between tabs or pages in a tabbed menu.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

⚡

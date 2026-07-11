# MenuSounds

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct MenuSounds
```

A collection of named sound events for standard menu interactions.

**Intent:** Provide a convenient bundle of UI sound events.

**Use-case:** Store a `MenuSounds` instance on a `MenuInfo` or `GenericMenuInfo<T>` so that navigation, submission, and cancellation all play the appropriate sounds automatically.

### ⭐ Properties
#### Cancel
```csharp
public readonly SoundEventId Cancel;
```

Sound event played when the player cancels or backs out of a menu.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
#### MenuSubmit
```csharp
public readonly SoundEventId MenuSubmit;
```

Sound event played when the player confirms a menu selection.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
#### OnError
```csharp
public readonly SoundEventId OnError;
```

Sound event played when the player attempts an invalid or unavailable action.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
#### SelectionChange
```csharp
public readonly SoundEventId SelectionChange;
```

Sound event played each time the highlighted menu item changes.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
#### TabSwitchChange
```csharp
public readonly SoundEventId TabSwitchChange;
```

Sound event played when switching between tabs or pages in a tabbed menu.

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \


⚡
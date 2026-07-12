# GamePreferences

**Namespace:** Murder.Save \
**Assembly:** Murder.dll

```csharp
public class GamePreferences
```

Tracks preferences of the current session. This is unique per run.
Used to track the game settings that are not tied to any game run (for example, volume).

**Intent:** Persists the player's device-level, non-save-slot settings — volume, language, fullscreen, screen shake, haptics, scaling and input bindings — to a single `.preferences` file under the game's save directory, independent of any particular save game.

**Use-case:** Access the live instance via `Game.Preferences` (`Game.Data.Preferences`). Read properties like `Fullscreen`, `AllVolume` or `Language` directly; use the `Set*` methods to change them, which both apply the new value and immediately persist it to disk via `OnPreferencesChanged`/`SaveSettings`. Subclass `GamePreferences` and override `OnPreferencesChangedImpl` if the game needs to react to preference changes (e.g. push the new volume to the audio engine) — see `Game.Fullscreen`, which reads `Preferences.Fullscreen` directly.

### ⭐ Constructors

```csharp
public GamePreferences()
```

Implicit parameterless constructor used both when creating the very first default preferences for a new install and when deserializing an existing `.preferences` file from disk. All properties start at their documented defaults until overwritten by deserialization or by calling one of the `Set*` methods.

### ⭐ Properties

#### AllVolume

```csharp
public float AllVolume { get; }
```

Master volume multiplier, in the range 0.0 (silent) to 1.0 (full), applied on top of `SoundVolume`/`MusicVolume`. Defaults to `0.8`. Change it with `SetAllVolume`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### AxisBindingsInfos

```csharp
public ImmutableArray<AxisBindingsInfo> AxisBindingsInfos { get; }
```

The player's custom analog axis (stick/trigger) input bindings, as previously captured by the input rebinding UI. Defaults to an empty array (meaning the engine's default axis bindings apply). Restored into `PlayerInput` on load.

**Returns** \
[ImmutableArray\<AxisBindingsInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### ButtonBindingsInfos

```csharp
public ImmutableArray<ButtonBindingsInfo> ButtonBindingsInfos { get; }
```

The player's custom button input bindings, as previously captured by the input rebinding UI. Defaults to an empty array (meaning the engine's default button bindings apply). Change it with `SetButtonBindingsInfos`; restored into `PlayerInput` on load.

**Returns** \
[ImmutableArray\<ButtonBindingsInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Fullscreen

```csharp
public bool Fullscreen { get; }
```

Whether the game window should run in fullscreen mode. Defaults to `true`. Change it with `SetFullScreen`; `Game.Fullscreen` reads this property directly.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Haptics

```csharp
public float Haptics { get; }
```

Controller/gamepad vibration intensity multiplier, in the range 0.0 (off) to 1.0 (full). Defaults to `1`. Change it with `SetHapticsMultiplier`; consumed by `HapticsManager` to scale rumble effects.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Language

```csharp
public LanguageId Language { get; }
```

The currently selected localization language. Defaults to `LanguageId.English`. Change it with `SetLanguage`.

**Returns** \
[LanguageId](../../Murder/Assets/Localization/LanguageId.html) \

#### MusicVolume

```csharp
public float MusicVolume { get; }
```

Music volume level, in the range 0.0 (silent) to 1.0 (full), independent of `SoundVolume`. Defaults to `1`. Change it with `SetMusicVolume`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Scaling

```csharp
public ScalingKind Scaling { get; }
```

The window/render scaling mode currently applied (auto, large, 1x/2x/3x pixel-perfect, or snap). Defaults to `ScalingKind.Auto`. Change it with `SetScalingKind`, which also resizes the game window to satisfy the chosen scale.

**Returns** \
[ScalingKind](../../Murder/Save/ScalingKind.html) \

#### ScreenShake

```csharp
public float ScreenShake { get; }
```

Screen shake intensity multiplier, in the range 0.0 (off) to 1.0 (full). Defaults to `1`. Change it with `SetScreenShakeMultiplier`; intended for players sensitive to camera shake effects.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SoundVolume

```csharp
public float SoundVolume { get; }
```

Sound effects volume level, in the range 0.0 (silent) to 1.0 (full), independent of `MusicVolume`. Defaults to `1`. Change it with `SetSoundVolume`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### OnPreferencesChangedImpl()

```csharp
public virtual void OnPreferencesChangedImpl()
```

Empty override point called by `OnPreferencesChanged` immediately before the preferences file is saved. Override this in a game-specific `GamePreferences` subclass to push newly changed values into live systems that don't poll preferences themselves (for example, applying the new volume to currently-playing sounds).

#### SetButtonBindingsInfos(ImmutableArray&lt;ButtonBindingsInfo&gt;)

```csharp
public void SetButtonBindingsInfos(ImmutableArray<ButtonBindingsInfo> buttonBindingsInfos)
```

Replaces `ButtonBindingsInfos` with `buttonBindingsInfos` and immediately saves preferences. Called by the input rebinding UI once the player finishes customizing their controls.

**Parameters** \
`buttonBindingsInfos` [ImmutableArray\<ButtonBindingsInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### SetFullScreen(bool)

```csharp
public bool SetFullScreen(bool value)
```

Sets `Fullscreen` to `value`, saves preferences, and returns the applied value. `Game.Fullscreen`'s setter calls this to keep the window mode and the persisted preference in sync.

**Parameters** \
`value` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetHapticsMultiplier(float)

```csharp
public float SetHapticsMultiplier(float value)
```

Sets `Haptics` to `value`, saves preferences, and returns the applied value.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetScreenShakeMultiplier(float)

```csharp
public float SetScreenShakeMultiplier(float value)
```

Sets `ScreenShake` to `value`, saves preferences, and returns the applied value.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetAllVolume(float)

```csharp
public float SetAllVolume(float value)
```

Sets `AllVolume` to `value`, saves preferences, and returns the applied value.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetMusicVolume(float)

```csharp
public float SetMusicVolume(float value)
```

Sets `MusicVolume` to `value`, saves preferences, and returns the applied value.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetSoundVolume(float)

```csharp
public float SetSoundVolume(float value)
```

Sets `SoundVolume` to `value`, saves preferences, and returns the applied value.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### OnPreferencesChanged()

```csharp
public void OnPreferencesChanged()
```

Called by every `Set*` method after applying a new value: invokes `OnPreferencesChangedImpl()` and then immediately calls `SaveSettings()` to persist the updated preferences to disk. Rarely called directly by game code — it exists mostly so subclasses only need to override `OnPreferencesChangedImpl` instead of re-implementing the save step themselves.

#### SetLanguage(LanguageId)

```csharp
public void SetLanguage(LanguageId id)
```

Sets `Language` to `id` and saves preferences (a no-op if `id` already equals the current language).

**Parameters** \
`id` [LanguageId](../../Murder/Assets/Localization/LanguageId.html) \

#### SetScalingKind(ScalingKind, bool)

```csharp
public void SetScalingKind(ScalingKind scaling, bool force)
```

Sets `Scaling` to `scaling` (a no-op if it already equals the current scaling and `force` is `false`) and resizes the game window to satisfy that scale's minimum size — e.g. `ScalingKind.OneX`/`TwoX`/`ThreeX` snap the window to an exact integer multiple of the base resolution when not fullscreen, while `ScalingKind.Auto`/`Large` just enforce a minimum size. Saves preferences afterwards.

**Parameters** \
`scaling` [ScalingKind](../../Murder/Save/ScalingKind.html) \
`force` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SaveSettings()

```csharp
protected void SaveSettings()
```

Serializes this `GamePreferences` instance and writes it to the `.preferences` file under `Game.Data.SaveBasePath`. Called automatically by `OnPreferencesChanged`; game code should not normally need to call it directly.

⚡

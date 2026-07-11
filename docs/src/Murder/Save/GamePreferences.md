# GamePreferences

**Namespace:** Murder.Save \
**Assembly:** Murder.dll

```csharp
public class GamePreferences
```

Tracks preferences of the current session. This is unique per run.
            Used to track the game settings that are not tied to any game run (for example, volume).

**Intent:** Stores player preferences that persist across game sessions.

**Use-case:** Access via `Game.Preferences` to read or write settings like volume and fullscreen mode; the engine serializes this automatically.

### ⭐ Constructors
```csharp
public GamePreferences()
```

### ⭐ Properties
#### _bloom
```csharp
protected bool _bloom;
```
Backing field for the bloom post-processing toggle.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### _downscale
```csharp
protected bool _downscale;
```
Backing field for the resolution downscale toggle.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### _language
```csharp
protected LanguageId _language;
```
Backing field for the current language preference.

**Returns** \
[LanguageId](../../Murder/Assets/Localization/LanguageId.html) \
#### _musicVolume
```csharp
protected float _musicVolume;
```
Backingfield for the music volume level (0.0–1.0).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### _soundVolume
```csharp
protected float _soundVolume;
```
Backing field for the sound effects volume level (0.0–1.0).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Language
```csharp
public LanguageId Language { get; }
```
The currently selected localization language.

**Returns** \
[LanguageId](../../Murder/Assets/Localization/LanguageId.html) \
#### MusicVolume
```csharp
public float MusicVolume { get; }
```
Music volume level in the range 0.0 (silent) to 1.0 (full).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### SoundVolume
```csharp
public float SoundVolume { get; }
```
Sound effects volume level in the range 0.0 (silent) to 1.0 (full).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### SaveSettings()
```csharp
protected void SaveSettings()
```
Serializes the current preferences to disk.

#### ToggleBloomAndSave()
```csharp
public bool ToggleBloomAndSave()
```
Flips the bloom post-processing toggle and immediately saves preferences; returns the new state.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ToggleDownscaleAndSave()
```csharp
public bool ToggleDownscaleAndSave()
```
Flips the resolution downscale toggle and immediately saves preferences; returns the new state.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetMusicVolume(float)
```csharp
public float SetMusicVolume(float value)
```
Sets the music volume to `value` and returns the applied value.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetSoundVolume(float)
```csharp
public float SetSoundVolume(float value)
```
Sets the sound effects volume to `value` and returns the applied value.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ToggleMusicVolumeAndSave()
```csharp
public float ToggleMusicVolumeAndSave()
```

This toggles the volume to the opposite of the current setting.
            Immediately serialize (and save) afterwards.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ToggleSoundVolumeAndSave()
```csharp
public float ToggleSoundVolumeAndSave()
```

This toggles the volume to the opposite of the current setting.
            Immediately serialize (and save) afterwards.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### OnPreferencesChangedImpl()
```csharp
public virtual void OnPreferencesChangedImpl()
```
Override point called after any preference change; use to apply changes to the audio or rendering subsystem.

#### OnPreferencesChanged()
```csharp
public void OnPreferencesChanged()
```
Notifies all listeners that a preference has changed and serializes settings to disk.

#### SetLanguage(LanguageId)
```csharp
public void SetLanguage(LanguageId id)
```
Changes the active language and saves the preference.

**Parameters** \
`id` [LanguageId](../../Murder/Assets/Localization/LanguageId.html) \



⚡
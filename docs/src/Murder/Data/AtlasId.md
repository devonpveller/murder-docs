# AtlasId

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public sealed enum AtlasId : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Identifies which texture atlas a sprite or asset belongs to.

**Use-case:** Use `AtlasId` values when loading or referencing a `TextureAtlas` so the engine fetches sprites from the correct packed atlas file. The `Description` attribute on each value maps to the actual atlas filename used at build time.

### ⭐ Properties
#### Cutscenes
```csharp
public static const AtlasId Cutscenes;
```
Atlas containing sprites used exclusively during cutscene playback.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \
#### Editor
```csharp
public static const AtlasId Editor;
```
Atlas containing editor-only UI icons and sprites; not shipped with the release build.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \
#### Gameplay
```csharp
public static const AtlasId Gameplay;
```
Main atlas packed with all gameplay sprites; loaded when entering a game scene.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \
#### None
```csharp
public static const AtlasId None;
```
Sentinel value indicating no atlas is assigned.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \
#### Preload
```csharp
public static const AtlasId Preload;
```
Atlas loaded during the initial preload phase before the main game loop begins.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \
#### Static
```csharp
public static const AtlasId Static;
```
Atlas for sprites that remain loaded across scenes and are never unloaded automatically.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \
#### Temporary
```csharp
public static const AtlasId Temporary;
```
Transient atlas that may be discarded between scenes or on demand.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \


⚡
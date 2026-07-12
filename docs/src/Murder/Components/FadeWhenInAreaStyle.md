# FadeWhenInAreaStyle

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
sealed enum FadeWhenInAreaStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Controls the fade behavior of a `FadeWhenInAreaComponent` when an entity enters or exits the trigger area. This is a nested enum declared inside [FadeWhenInAreaComponent](../../Murder/Components/FadeWhenInAreaComponent.html); it is only meaningful when read from that component's `Style` field.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Lets a level or content author pick which of the three fade behaviors an area-triggered fade should use, without needing three separate component types.

**Use-case:** Set on `FadeWhenInAreaComponent.Style` in the editor; use `HideWhenInArea` for foliage or foreground props that should become transparent while the player is behind/under them, `ShowWhenInArea` for reveal effects, and `HideForeverAfterInArea` for a one-time transparency change (e.g. a wall that disappears permanently once the player has passed through it once).

### ⭐ Properties

#### HideForeverAfterInArea

```csharp
public static const FadeWhenInAreaStyle HideForeverAfterInArea;
```

The entity fades out the first time a triggering entity enters the area and remains hidden permanently afterward.

**Returns** \
[FadeWhenInAreaStyle](../../Murder/Components/FadeWhenInAreaStyle.html) \

#### HideWhenInArea

```csharp
public static const FadeWhenInAreaStyle HideWhenInArea;
```

The entity fades out (becomes transparent) while a triggering entity is inside the area, and fades back in when it leaves. This is the default value.

**Returns** \
[FadeWhenInAreaStyle](../../Murder/Components/FadeWhenInAreaStyle.html) \

#### ShowWhenInArea

```csharp
public static const FadeWhenInAreaStyle ShowWhenInArea;
```

The entity fades in (becomes visible) while a triggering entity is inside the area, and fades back out when it leaves.

**Returns** \
[FadeWhenInAreaStyle](../../Murder/Components/FadeWhenInAreaStyle.html) \

⚡

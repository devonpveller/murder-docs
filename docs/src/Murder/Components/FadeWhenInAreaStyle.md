# FadeWhenInAreaStyle

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
sealed enum FadeWhenInAreaStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Controls the fade behavior of a `FadeWhenInAreaComponent` when an entity enters or exits the trigger area.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Determines whether the entity fades out while inside the area, fades in while inside it, or stays hidden permanently after the player first enters.

**Use-case:** Set on `FadeWhenInAreaComponent.Style`; use `HideWhenInArea` for foliage that should become transparent when the player is underneath it, `ShowWhenInArea` for reveals, and `HideForeverAfterInArea` for one-time transparency effects.

### ⭐ Properties
#### HideWhenInArea
```csharp
public static const FadeWhenInAreaStyle HideWhenInArea;
```

The entity fades out (becomes transparent) while a triggering entity is inside the area, and fades back in when they leave.

**Returns** \
[FadeWhenInAreaStyle](../../Murder/Components/FadeWhenInAreaStyle.html) \
#### HideForeverAfterInArea
```csharp
public static const FadeWhenInAreaStyle HideForeverAfterInArea;
```

The entity fades out the first time a triggering entity enters the area and remains hidden permanently.

**Returns** \
[FadeWhenInAreaStyle](../../Murder/Components/FadeWhenInAreaStyle.html) \
#### ShowWhenInArea
```csharp
public static const FadeWhenInAreaStyle ShowWhenInArea;
```

The entity fades in (becomes visible) while a triggering entity is inside the area, and fades back out when they leave.

**Returns** \
[FadeWhenInAreaStyle](../../Murder/Components/FadeWhenInAreaStyle.html) \


⚡
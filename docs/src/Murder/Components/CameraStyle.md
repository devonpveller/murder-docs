# CameraStyle

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed enum CameraStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies how the camera interpolates toward its follow target.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Controls the camera follow algorithm so designers can choose the right feel for each gameplay context.

**Use-case:** Set via `CameraFollowComponent.Style` when the entity is created; for example use `DeadZone` for normal gameplay, `Center` for cutscenes, and `Perfect` for pixel-perfect movement.

### ⭐ Properties
#### Center
```csharp
public static const CameraStyle Center;
```

Camera is always centered on the target with no dead zone or lag.

**Returns** \
[CameraStyle](../../Murder/Components/CameraStyle.html) \
#### DeadZone
```csharp
public static const CameraStyle DeadZone;
```

Camera follows the target but only moves once the target exits the dead zone, providing a looser, more organic feel.

**Returns** \
[CameraStyle](../../Murder/Components/CameraStyle.html) \
#### Perfect
```csharp
public static const CameraStyle Perfect;
```

Camera tracks the target pixel-perfectly with no smoothing or dead zone.

**Returns** \
[CameraStyle](../../Murder/Components/CameraStyle.html) \


⚡
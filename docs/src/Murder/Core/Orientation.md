# Orientation

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed enum Orientation : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Enumerates the spatial axes an entity, animation, or movement can be described in terms of.

**Intent:** A simple three-value enum that encodes whether something operates along the horizontal axis, the vertical axis, or both. Used together with `OrientationHelper` to classify a movement/velocity vector as primarily horizontal or vertical, or to explicitly represent "both axes apply" cases (e.g. an isometric or 8-directional facing).

**Use-case:** Pass to `OrientationHelper.GetOrientationAmount` to measure how much of a movement vector's magnitude is attributable to a given axis, use `OrientationHelper.GetDominantOrientation` to extract the dominant axis of a movement vector, or store on a component to indicate which axis (or both) an entity currently cares about for animation/collision purposes.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Both

```csharp
public static const Orientation Both;
```

Both axes apply/matter; not restricted to a single dominant direction. `OrientationHelper.GetOrientationAmount` always returns `1` for this value, since there is no single axis to measure a fraction against.

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \

#### Horizontal

```csharp
public static const Orientation Horizontal;
```

The entity or movement is oriented along the X axis.

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \

#### Vertical

```csharp
public static const Orientation Vertical;
```

The entity or movement is oriented along the Y axis.

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \

⚡

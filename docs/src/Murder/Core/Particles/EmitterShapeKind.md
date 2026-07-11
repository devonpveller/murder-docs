# EmitterShapeKind

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed enum EmitterShapeKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies the geometric shape from which an emitter spawns particles.

**Intent:** Select the particle-origin geometry for an `EmitterShape`.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Circle
```csharp
public static const EmitterShapeKind Circle;
```

Particles spawn from random points inside the circle area.

**Returns** \
[EmitterShapeKind](../../../Murder/Core/Particles/EmitterShapeKind.html) \
#### CircleOutline
```csharp
public static const EmitterShapeKind CircleOutline;
```

Particles spawn from random points on the circle's perimeter.

**Returns** \
[EmitterShapeKind](../../../Murder/Core/Particles/EmitterShapeKind.html) \
#### Line
```csharp
public static const EmitterShapeKind Line;
```

Particles spawn at random positions along a line segment.

**Returns** \
[EmitterShapeKind](../../../Murder/Core/Particles/EmitterShapeKind.html) \
#### Point
```csharp
public static const EmitterShapeKind Point;
```

All particles spawn from a single central point.

**Returns** \
[EmitterShapeKind](../../../Murder/Core/Particles/EmitterShapeKind.html) \
#### Rectangle
```csharp
public static const EmitterShapeKind Rectangle;
```

Particles spawn from random points within a rectangular area.

**Returns** \
[EmitterShapeKind](../../../Murder/Core/Particles/EmitterShapeKind.html) \


⚡
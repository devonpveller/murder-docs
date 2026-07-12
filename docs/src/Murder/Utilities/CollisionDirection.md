# CollisionDirection

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed enum CollisionDirection : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Distinguishes the two phases of a collision event so handlers know whether an entity is entering or exiting a trigger zone.

**Intent:** Provides a clear two-state flag passed with `OnCollisionMessage` so collision handlers can branch on enter vs. exit.

**Use-case:** Read in messager systems (e.g., `InteractOnCollisionSystem`, `AgentMovementModifierSystem`) to decide whether to apply or remove an effect.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Enter

```csharp
public static const CollisionDirection Enter;
```

The colliding entity has just entered the trigger zone.

**Returns** \
[CollisionDirection](../../Murder/Utilities/CollisionDirection.html) \

#### Exit

```csharp
public static const CollisionDirection Exit;
```

The colliding entity has just left the trigger zone.

**Returns** \
[CollisionDirection](../../Murder/Utilities/CollisionDirection.html) \

⚡

# TargetEntity

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed enum TargetEntity : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies which entity an interaction or action targets relative to the entity that owns the component.

**Intent:** Provides a declarative way for interaction components to direct actions at the owner, its parent, its children, the interacting agent, or a new entity.

**Use-case:** Set on interaction or action components to control which entity receives the effect when the interaction fires.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Child
```csharp
public static const TargetEntity Child;
```

The action targets a child entity of the owner.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \
#### CreateNewEntity
```csharp
public static const TargetEntity CreateNewEntity;
```

The action spawns and targets a brand-new entity.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \
#### Interactor
```csharp
public static const TargetEntity Interactor;
```

The action targets the entity that initiated the interaction.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \
#### Parent
```csharp
public static const TargetEntity Parent;
```

The action targets the entity's parent.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \
#### Self
```csharp
public static const TargetEntity Self;
```

The action targets the entity that owns the component.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \
#### Target
```csharp
public static const TargetEntity Target;
```

The action targets a specifically designated target entity.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \


⚡
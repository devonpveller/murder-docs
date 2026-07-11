# RemoveStyle

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed enum RemoveStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Describes the method used to remove or deactivate an entity when a timed or conditional removal is triggered.

**Intent:** Give designers fine-grained control over what happens to an entity when it is "removed" — ranging from full destruction to simply hiding it.

**Use-case:** Set on components such as `DestroyAtTimeComponent` to specify whether an entity should be fully destroyed, deactivated, or just have its components stripped.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Deactivate
```csharp
public static const RemoveStyle Deactivate;
```

Deactivates the entity (hides it) without fully destroying it.

**Returns** \
[RemoveStyle](../../Murder/Components/RemoveStyle.html) \
#### Destroy
```csharp
public static const RemoveStyle Destroy;
```

Fully destroys the entity, removing it from the world permanently.

**Returns** \
[RemoveStyle](../../Murder/Components/RemoveStyle.html) \
#### None
```csharp
public static const RemoveStyle None;
```

No removal action is taken.

**Returns** \
[RemoveStyle](../../Murder/Components/RemoveStyle.html) \
#### RemoveComponents
```csharp
public static const RemoveStyle RemoveComponents;
```

Strips the associated components from the entity but leaves the entity itself in the world.

**Returns** \
[RemoveStyle](../../Murder/Components/RemoveStyle.html) \


⚡
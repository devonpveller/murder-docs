# RemoveStyle

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed enum RemoveStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Describes how an entity should be taken out of play once a timed removal (e.g. [DestroyAtTimeComponent](../../Murder/Components/DestroyAtTimeComponent.html)) triggers.

**Intent:** Give designers fine-grained control over what happens to an entity when it is "removed" — ranging from full destruction to simply deactivating it.

**Use-case:** Set via `DestroyAtTimeComponent.Style` to control how an expiring entity is handled. Note that as of `DestroyAtTimeSystem`, only `Destroy` and `Deactivate` are actually handled; `RemoveComponents` is defined for future use but currently falls through to the same no-op branch as `None`.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Destroy

```csharp
public static const RemoveStyle Destroy;
```

Fully destroys the entity, removing it from the world permanently. This is the default value of `DestroyAtTimeComponent.Style`.

**Returns** \
[RemoveStyle](../../Murder/Components/RemoveStyle.html) \

#### Deactivate

```csharp
public static const RemoveStyle Deactivate;
```

Deactivates the entity (removing it from active simulation/rendering) without destroying it, so it can potentially be reactivated later.

**Returns** \
[RemoveStyle](../../Murder/Components/RemoveStyle.html) \

#### RemoveComponents

```csharp
public static const RemoveStyle RemoveComponents;
```

Intended to strip the associated components from the entity while leaving the entity itself in the world. Not yet implemented by `DestroyAtTimeSystem`, which currently treats this the same as `None` (no action taken).

**Returns** \
[RemoveStyle](../../Murder/Components/RemoveStyle.html) \

#### None

```csharp
public static const RemoveStyle None;
```

No removal action is taken when the timer expires.

**Returns** \
[RemoveStyle](../../Murder/Components/RemoveStyle.html) \

⚡

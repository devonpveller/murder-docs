# AddChildProperties

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed enum AddChildProperties : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags that control optional side-effects applied by [AddChildOnInteraction](../../Murder/Interactions/AddChildOnInteraction.html) when it spawns and attaches a new child entity.

**Intent:** Configures optional side-effects when attaching a new child entity to an interacted entity.

**Use-case:** Pass `SendEventComponentToParent` to ensure that animation events registered on the spawned child are also handled by the parent entity, allowing centralized event processing.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### None

```csharp
public static const AddChildProperties None;
```

The child is attached with no additional side-effects.

**Returns** \
[AddChildProperties](../../Murder/Interactions/AddChildProperties.html) \

#### SendEventComponentToParent

```csharp
public static const AddChildProperties SendEventComponentToParent;
```

After the child is attached, its `EventListenerComponent` (if any) is merged into the parent's own event listener and removed from the child, so the parent receives the child's animation/events. Useful when the child is a purely visual sub-entity whose events should be handled by the owning entity's logic.

**Returns** \
[AddChildProperties](../../Murder/Interactions/AddChildProperties.html) \

⚡

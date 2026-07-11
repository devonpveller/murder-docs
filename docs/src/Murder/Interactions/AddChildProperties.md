# AddChildProperties

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed enum AddChildProperties : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags that control the behaviour of [AddChildOnInteraction](../../Murder/Interactions/AddChildOnInteraction.html) when a child entity is spawned.

**Intent:** Configures optional side-effects when attaching a new child entity to an interacted entity.

**Use-case:** Pass `SendEventComponentToParent` to ensure that animation events registered on the spawned child are also handled by the parent entity, allowing centralized event processing.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### None
```csharp
public static const AddChildProperties None;
```
No additional behaviour; the child is simply added without any extra side-effects.

**Returns** \
[AddChildProperties](../../Murder/Interactions/AddChildProperties.html) \
#### SendEventComponentToParent
```csharp
public static const AddChildProperties SendEventComponentToParent;
```
Copies the child's `EventListenerComponent` to the parent so the parent receives the child's animation events.

**Returns** \
[AddChildProperties](../../Murder/Interactions/AddChildProperties.html) \


⚡
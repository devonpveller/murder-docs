# DestroyWho

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed enum DestroyWho : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies which entity is destroyed when a [RemoveEntityOnInteraction](../../Murder/Interactions/RemoveEntityOnInteraction.html) fires.

**Intent:** Selects the destruction target relative to the entities involved in an interaction.

**Use-case:** Configure `RemoveEntityOnInteraction` to cleanly despawn the interacted entity, its parent, the interactor, or its children depending on the game logic required.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Children
```csharp
public static const DestroyWho Children;
```
Destroys the first child of the interacted entity.

**Returns** \
[DestroyWho](../../Murder/Interactions/DestroyWho.html) \
#### Interacted
```csharp
public static const DestroyWho Interacted;
```
Destroys the entity that was interacted with.

**Returns** \
[DestroyWho](../../Murder/Interactions/DestroyWho.html) \
#### Interactor
```csharp
public static const DestroyWho Interactor;
```
Destroys the entity that initiated the interaction.

**Returns** \
[DestroyWho](../../Murder/Interactions/DestroyWho.html) \
#### None
```csharp
public static const DestroyWho None;
```
No entity is destroyed; the interaction fires without any destruction side-effect.

**Returns** \
[DestroyWho](../../Murder/Interactions/DestroyWho.html) \
#### Parent
```csharp
public static const DestroyWho Parent;
```
Destroys the parent of the interacted entity.

**Returns** \
[DestroyWho](../../Murder/Interactions/DestroyWho.html) \
#### Target
```csharp
public static const DestroyWho Target;
```
Destroys the entity referenced by the interacted entity's `IdTarget` or `IdTargetCollection` component.

**Returns** \
[DestroyWho](../../Murder/Interactions/DestroyWho.html) \


⚡
# AddEntityFlags

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed enum AddEntityFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags that control how [AddEntityOnInteraction](../../Murder/Interactions/AddEntityOnInteraction.html) positions the entity it spawns and whether it removes the triggering interaction afterwards.

**Intent:** Configures the spawn positioning and one-shot behaviour of `AddEntityOnInteraction`.

**Use-case:** Combine `FromInteractor`/`FromInteracted` to place the spawned entity where the interaction happened, and add `RemoveAfterTriggered` for spawners that should only ever fire once.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### FromInteracted

```csharp
public static const AddEntityFlags FromInteracted;
```

The spawned entity is placed at the interacted entity's current global position.

**Returns** \
[AddEntityFlags](../../Murder/Interactions/AddEntityFlags.html) \

#### FromInteractor

```csharp
public static const AddEntityFlags FromInteractor;
```

The spawned entity is placed at the interactor's current global position.

**Returns** \
[AddEntityFlags](../../Murder/Interactions/AddEntityFlags.html) \

#### None

```csharp
public static const AddEntityFlags None;
```

The spawned entity keeps whatever position its prefab defines; no positioning or cleanup happens.

**Returns** \
[AddEntityFlags](../../Murder/Interactions/AddEntityFlags.html) \

#### RemoveAfterTriggered

```csharp
public static const AddEntityFlags RemoveAfterTriggered;
```

After spawning, the interactive component that triggered this interaction is removed from the interacted entity, so the interaction only ever fires once. Useful for one-shot spawners.

**Returns** \
[AddEntityFlags](../../Murder/Interactions/AddEntityFlags.html) \

⚡

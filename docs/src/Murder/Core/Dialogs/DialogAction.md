# DialogAction

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct DialogAction
```

Describes a single side-effect to execute when a `Dialog` node is visited: writing a value to a blackboard fact or applying a component to an entity.

**Intent:** Bundles together the target fact, the operation kind (`BlackboardActionKind`), and the typed value payload so the dialogue system can mutate world state as dialogue plays.

**Use-case:** Add `DialogAction` entries to `Dialog.Actions`; the runtime processes them in order when the node is visited, updating blackboards or entity components accordingly.

### ⭐ Constructors

```csharp
public DialogAction()
```

Creates an empty action with default values.

```csharp
public DialogAction(int id, Fact fact, BlackboardActionKind kind, string string, T? int, T? bool, T? float, IComponent component)
```

Full constructor; only the value field matching `fact.Kind` is stored — all others are cleared.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`fact` [Fact](../../../Murder/Core/Dialogs/Fact.html) \
`kind` [BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \
`string` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`int` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`bool` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`float` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`component` [IComponent](../../../Bang/Components/IComponent.html) \

### ⭐ Properties

#### BoolValue

```csharp
public readonly T? BoolValue;
```

The boolean value applied to the fact when `Kind` is `Set` or `Toggle` on a `Bool` fact.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### ComponentValue

```csharp
public readonly IComponent ComponentValue;
```

The component instance applied to the target entity when `Kind` is `Component`.

**Returns** \
[IComponent](../../../Bang/Components/IComponent.html) \

#### Fact

```csharp
public readonly Fact Fact;
```

The blackboard variable this action writes to.

**Returns** \
[Fact](../../../Murder/Core/Dialogs/Fact.html) \

#### FloatValue

```csharp
public readonly T? FloatValue;
```

The float value applied when the fact is of kind `Float`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Id

```csharp
public readonly int Id;
```

Unique identifier for this action within its dialog node, used for editor tracking.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### IntValue

```csharp
public readonly T? IntValue;
```

The integer value applied when the fact is of kind `Int` or `Weight`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Kind

```csharp
public readonly BlackboardActionKind Kind;
```

The mutation operation to apply (`Set`, `Add`, `Toggle`, `Component`, etc.).

**Returns** \
[BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \

#### StrValue

```csharp
public readonly string StrValue;
```

The string value applied when the fact is of kind `String`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### WithComponent(IComponent)

```csharp
public DialogAction WithComponent(IComponent c)
```

Returns a copy of this action with the `ComponentValue` replaced.

**Parameters** \
`c` [IComponent](../../../Bang/Components/IComponent.html) \

**Returns** \
[DialogAction](../../../Murder/Core/Dialogs/DialogAction.html) \

#### WithFact(Fact)

```csharp
public DialogAction WithFact(Fact fact)
```

Returns a copy of this action with the `Fact` replaced.

**Parameters** \
`fact` [Fact](../../../Murder/Core/Dialogs/Fact.html) \

**Returns** \
[DialogAction](../../../Murder/Core/Dialogs/DialogAction.html) \

#### WithKind(BlackboardActionKind)

```csharp
public DialogAction WithKind(BlackboardActionKind kind)
```

Returns a copy of this action with the `Kind` replaced.

**Parameters** \
`kind` [BlackboardActionKind](../../../Murder/Core/Dialogs/BlackboardActionKind.html) \

**Returns** \
[DialogAction](../../../Murder/Core/Dialogs/DialogAction.html) \

⚡

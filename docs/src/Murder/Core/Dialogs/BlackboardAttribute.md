# BlackboardAttribute

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public class BlackboardAttribute : Attribute
```

Marks a class as a named blackboard type that the editor and engine can discover.

**Intent:** Registers a blackboard implementation under a stable string name so the dialogue system and editor tools can enumerate, serialize, and look up available blackboards by name.

**Use-case:** Apply `[Blackboard("MyBoard")]` to a class that implements `IBlackboard`; the engine will automatically associate it with that name and (optionally) treat it as the default blackboard when `isDefault` is `true`.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public BlackboardAttribute(string name, bool default)
```

Creates the attribute with an explicit name and marks whether this blackboard is the default one.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`default` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public BlackboardAttribute(string name)
```

Creates the attribute with the given name; `IsDefault` will be `false`.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### IsDefault
```csharp
public readonly bool IsDefault;
```

When `true`, this blackboard is the fallback used when no explicit blackboard name is specified during a fact lookup.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Name
```csharp
public readonly string Name;
```

The unique string identifier for this blackboard type, used by the dialogue system to locate the correct blackboard at runtime.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Inherited from `Attribute`; returns a unique object that identifies this attribute type instance.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
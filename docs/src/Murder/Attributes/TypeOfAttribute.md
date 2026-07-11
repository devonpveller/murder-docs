# TypeOfAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class TypeOfAttribute : Attribute
```

Attribute for looking on a [TypeOfAttribute.Type](../../Murder/Attributes/TypeOfAttribute.html#type) with specific properties.

**Intent:** Mark a `Type` field so the editor presents a filtered type browser showing only concrete implementations of a given base type.

**Use-case:** Apply to `Type` fields in components or assets that reference a specific class implementation, such as an AI state machine class or a custom interaction handler. The editor will display a picker restricted to types that inherit from or implement the specified base type.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public TypeOfAttribute(Type type)
```

Creates a new [TypeOfAttribute](../../Murder/Attributes/TypeOfAttribute.html).

**Parameters** \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
\

### ⭐ Properties
#### Type
```csharp
public readonly Type Type;
```

The base type whose concrete implementations are shown in the editor type picker for the decorated field.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
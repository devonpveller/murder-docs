# TypeOfAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class TypeOfAttribute : Attribute
```

Attribute for looking on a [TypeOfAttribute.Type](../../Murder/Attributes/TypeOfAttribute.html#type) with specific properties.

**Intent:** Mark a `Type`-typed field so the editor knows which kind of type-search box to open and, where applicable, restrict it to implementations/subtypes of a given base type.

**Use-case:** Has two concrete consumers in the editor. On a single field typed `IStateMachineComponent`, `IComponentField` reads `TypeOfAttribute.Type` and passes it as the `subtypeOf` filter to `SearchBox.SearchStateMachines`, so only state machines deriving from that base type appear in the picker. On an `ImmutableArray<Type>` field, `ImmutableArrayTypeField` requires `TypeOfAttribute.Type` to be exactly `typeof(IComponent)` or `typeof(ISystem)` to decide whether new entries are added via the component search box or the system search box (any other type is unsupported and renders an error in the inspector).

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

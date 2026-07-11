# GeneratesAttribute

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public class GeneratesAttribute : Attribute
```

Marks a component that generates another component in runtime. This is used to satisfy the
`[Requires(...)]` dependency check performed when an entity is added to the world (see
[RequiresAttribute](../../Bang/Components/RequiresAttribute.html)): if a component `A` requires a
component `B`, but the entity does not actually have `B`, Bang looks at `B`'s
[GeneratesAttribute](../../Bang/Components/GeneratesAttribute.html) — if `B` is decorated with
`[Generates(typeof(C))]` and the entity has `C` instead, the dependency is still considered
satisfied. This lets a "source" component that is only used to *produce* another component at
runtime (for example, a component read once by a factory system to build a derived, more
specialized component) stand in for the component it generates without failing entity validation.
Apply this attribute to the *source* component, passing the *generated* component's `Type` as the
constructor argument.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public GeneratesAttribute(Type type)
```

Creates a new [GeneratesAttribute](../../Bang/Components/GeneratesAttribute.html).

**Parameters** \
`type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
\

### ⭐ Properties
#### Type
```csharp
public Type Type { get; public set; }
```

Component which will be generated from the component that has this attribute.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
# CustomNameAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class CustomNameAttribute : Attribute
```

Overrides the auto-generated display name the editor would otherwise derive from a type or member name.

**Intent:** Gives components, interactions, and other reflected types/members a friendlier, often icon-prefixed label in the editor instead of their raw C# name.

**Use-case:** Apply to a component or interaction struct (or a field) to replace the label the editor derives via `Prettify.FormatName`/`ReflectionHelper.GetGenericName` with an explicit one, e.g. `[CustomName($" {nameof(AmbienceComponent)}")]` on `AmbienceComponent`, or `[CustomName(" Collider")]` on `ColliderComponent`. The inspector header, the "Add Component" list, and per-field labels all read this attribute when present.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public CustomNameAttribute(string name)
```

Creates the attribute with the given custom display name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Name

```csharp
public string Name;
```

The display name shown by the editor in place of the auto-generated label.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

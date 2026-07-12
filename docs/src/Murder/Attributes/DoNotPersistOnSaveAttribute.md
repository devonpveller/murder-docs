# DoNotPersistOnSaveAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class DoNotPersistOnSaveAttribute : Attribute
```

Marks a component so it is excluded from save-game serialization, with an optional override condition.

**Intent:** Prevent a specific component from being written to the save file, keeping runtime-only state out of persisted data.

**Use-case:** Apply to components that hold transient runtime data (such as cached pathfinding results, active animation state, or physics velocities). Pass a component type to `ExceptIfComponentIsPresent` to re-enable persistence conditionally when the entity also carries that component.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public DoNotPersistOnSaveAttribute()
```

Creates a new instance that unconditionally excludes the component from save serialization.

```csharp
public DoNotPersistOnSaveAttribute(Type exceptIfComponentIsPresent)
```

Creates a new instance that excludes the component unless the entity also has the specified component type.

**Parameters** \
`exceptIfComponentIsPresent` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

### ⭐ Properties

#### ExceptIfComponentIsPresent

```csharp
public readonly Type ExceptIfComponentIsPresent;
```

This will dismiss this attribute and persist the component on the serialization if the following IComponent type is present.

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

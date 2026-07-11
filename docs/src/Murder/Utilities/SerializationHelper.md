# SerializationHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class SerializationHelper
```

Utilities for JSON serialization configuration and deep-copying serializable objects using `System.Text.Json`.

**Intent:** Provides helpers for composing JSON resolver modifier chains and for creating deep clones of serializable objects.

**Use-case:** Use `DeepCopy<T>` to clone components or assets, `WithModifiers` to extend a type-info resolver, and `ApplyModifierForPrivateFieldsAndGetters` to enable private-member serialization.

### ⭐ Methods
#### WithModifiers(IJsonTypeInfoResolver, Action`1[])
```csharp
public IJsonTypeInfoResolver WithModifiers(IJsonTypeInfoResolver resolver, Action`1[] modifiers)
```

Wraps a `IJsonTypeInfoResolver` with additional modifier delegates that can customize per-type serialization behavior.

**Parameters** \
`resolver` [IJsonTypeInfoResolver](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.Metadata.IJsonTypeInfoResolver?view=net-7.0) \
`modifiers` [Action\<T\>[]](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \

**Returns** \
[IJsonTypeInfoResolver](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.Metadata.IJsonTypeInfoResolver?view=net-7.0) \

#### DeepCopy(T)
```csharp
public T DeepCopy(T c)
```

Creates a deep copy of the given object by serializing it to JSON and deserializing a fresh instance.

**Parameters** \
`c` [T](../../) \

**Returns** \
[T](../../) \

#### ApplyModifierForPrivateFieldsAndGetters(JsonTypeInfo)
```csharp
public void ApplyModifierForPrivateFieldsAndGetters(JsonTypeInfo jsonTypeInfo)
```

A `System.Text.Json` modifier that enables serialization of private fields and getter-only properties on the given type.

**Parameters** \
`jsonTypeInfo` [JsonTypeInfo](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.Metadata.JsonTypeInfo?view=net-7.0) \



⚡
# MurderSerializerOptionsExtensions

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public static class MurderSerializerOptionsExtensions
```

Provides a json serializer that supports all the serializable types in Murder.

**Intent:** Provides pre-configured `JsonSerializerOptions` with all Murder custom converters registered.

**Use-case:** Reference `MurderSerializerOptionsExtensions.Options` wherever you need to serialize or deserialize Murder types with `System.Text.Json`.

### ⭐ Properties
#### Options
```csharp
public readonly static JsonSerializerOptions Options;
```

Default options that should be used when serializing or deserializing any components
            within the project.

**Returns** \
[JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \


⚡
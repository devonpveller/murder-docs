# JsonTypeConverter

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public class JsonTypeConverter : JsonConverter<T>
```

Custom `JsonConverter<Type>` that serializes CLR `Type` objects as their assembly-qualified name string.

**Intent:** Allows `System.Type` references to be round-tripped through JSON so that component type registries and asset type metadata can be persisted.

**Use-case:** Registered automatically in `MurderSerializerOptionsExtensions.Options`; do not call directly unless building a custom serializer pipeline.

**Implements:** _[JsonConverter\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.JsonConverter-1?view=net-7.0)_

### ⭐ Constructors
```csharp
public JsonTypeConverter()
```
Creates a new `JsonTypeConverter` instance.

### ⭐ Properties
#### HandleNull
```csharp
public virtual bool HandleNull { get; }
```
Returns `false`; `null` types are not expected and will throw during deserialization.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Type
```csharp
public virtual Type Type { get; }
```
The type this converter handles (`System.Type`).

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
### ⭐ Methods
#### CanConvert(Type)
```csharp
public virtual bool CanConvert(Type typeToConvert)
```
Returns `true` when `typeToConvert` is `System.Type` or a subclass.

**Parameters** \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Read(Utf8JsonReader&, Type, JsonSerializerOptions)
```csharp
public virtual Type Read(Utf8JsonReader& reader, Type typeToConvert, JsonSerializerOptions options)
```
Deserializes a `Type` by reading its assembly-qualified name from the JSON stream.

**Parameters** \
`reader` [Utf8JsonReader&](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonReader?view=net-7.0) \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### ReadAsPropertyName(Utf8JsonReader&, Type, JsonSerializerOptions)
```csharp
public virtual Type ReadAsPropertyName(Utf8JsonReader& reader, Type typeToConvert, JsonSerializerOptions options)
```
Deserializes a `Type` from a JSON property name token.

**Parameters** \
`reader` [Utf8JsonReader&](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonReader?view=net-7.0) \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### Write(Utf8JsonWriter, Type, JsonSerializerOptions)
```csharp
public virtual void Write(Utf8JsonWriter writer, Type value, JsonSerializerOptions options)
```
Serializes a `Type` by writing its assembly-qualified name as a JSON string value.

**Parameters** \
`writer` [Utf8JsonWriter](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonWriter?view=net-7.0) \
`value` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

#### WriteAsPropertyName(Utf8JsonWriter, Type, JsonSerializerOptions)
```csharp
public virtual void WriteAsPropertyName(Utf8JsonWriter writer, Type value, JsonSerializerOptions options)
```
Serializes a `Type` as a JSON property name using its assembly-qualified name.

**Parameters** \
`writer` [Utf8JsonWriter](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonWriter?view=net-7.0) \
`value` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

#### GetDefaultConverterStrategy()
```csharp
virtual ConverterStrategy GetDefaultConverterStrategy()
```

**Returns** \
[ConverterStrategy](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.ConverterStrategy?view=net-7.0) \



⚡
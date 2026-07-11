# ComplexDictionaryConverter\<T, V\>

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public sealed class ComplexDictionaryConverter<T, V> : JsonConverter<T>
```

Custom `JsonConverter` for `ComplexDictionary<TKey, TValue>` that handles non-string dictionary keys by serializing them as JSON arrays of `[key, value]` pairs.

**Intent:** Works around the `System.Text.Json` limitation that only allows `string`-typed dictionary keys by providing explicit read/write logic.

**Use-case:** Registered automatically in `MurderSerializerOptionsExtensions.Options`; no manual use is needed in game code.

**Implements:** _[JsonConverter\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.JsonConverter-1?view=net-7.0)_

### ⭐ Constructors
```csharp
public ComplexDictionaryConverter<T, V>()
```
Creates a new converter instance.

### ⭐ Properties
#### HandleNull
```csharp
public virtual bool HandleNull { get; }
```
Returns `false`; this converter does not handle `null` values for the dictionary type.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Type
```csharp
public virtual Type Type { get; }
```
The generic `ComplexDictionary` type this converter handles.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
### ⭐ Methods
#### CanConvert(Type)
```csharp
public virtual bool CanConvert(Type typeToConvert)
```
Returns `true` if `typeToConvert` is a `ComplexDictionary<TKey, TValue>`.

**Parameters** \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Read(Utf8JsonReader&, Type, JsonSerializerOptions)
```csharp
public virtual ComplexDictionary<TKey, TValue> Read(Utf8JsonReader& reader, Type typeToConvert, JsonSerializerOptions options)
```
Deserializes a `ComplexDictionary` from the JSON stream, reading key-value pairs with non-string key support.

**Parameters** \
`reader` [Utf8JsonReader&](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonReader?view=net-7.0) \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

**Returns** \
[ComplexDictionary\<TKey, TValue\>](../../Murder/Serialization/ComplexDictionary-2.html) \

#### ReadAsPropertyName(Utf8JsonReader&, Type, JsonSerializerOptions)
```csharp
public virtual ComplexDictionary<TKey, TValue> ReadAsPropertyName(Utf8JsonReader& reader, Type typeToConvert, JsonSerializerOptions options)
```
Deserializes a `ComplexDictionary` when it appears as a JSON property name.

**Parameters** \
`reader` [Utf8JsonReader&](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonReader?view=net-7.0) \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

**Returns** \
[ComplexDictionary\<TKey, TValue\>](../../Murder/Serialization/ComplexDictionary-2.html) \

#### Write(Utf8JsonWriter, ComplexDictionary<TKey, TValue>, JsonSerializerOptions)
```csharp
public virtual void Write(Utf8JsonWriter writer, ComplexDictionary<TKey, TValue> dictionary, JsonSerializerOptions options)
```
Serializes the `ComplexDictionary` to JSON, writing non-string keys as serialized objects.

**Parameters** \
`writer` [Utf8JsonWriter](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonWriter?view=net-7.0) \
`dictionary` [ComplexDictionary\<TKey, TValue\>](../../Murder/Serialization/ComplexDictionary-2.html) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

#### WriteAsPropertyName(Utf8JsonWriter, ComplexDictionary<TKey, TValue>, JsonSerializerOptions)
```csharp
public virtual void WriteAsPropertyName(Utf8JsonWriter writer, ComplexDictionary<TKey, TValue> value, JsonSerializerOptions options)
```
Serializes the `ComplexDictionary` as a property name in a JSON object.

**Parameters** \
`writer` [Utf8JsonWriter](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonWriter?view=net-7.0) \
`value` [ComplexDictionary\<TKey, TValue\>](../../Murder/Serialization/ComplexDictionary-2.html) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

#### GetDefaultConverterStrategy()
```csharp
virtual ConverterStrategy GetDefaultConverterStrategy()
```

**Returns** \
[ConverterStrategy](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.ConverterStrategy?view=net-7.0) \



⚡
# JsonTypeConverter

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public class JsonTypeConverter : JsonConverter<Type>
```

`JsonConverter<Type>` that lets a raw CLR `Type` reference be serialized to and from JSON by writing/reading its `Type.AssemblyQualifiedName` as a string.

**Intent:** `System.Text.Json` has no built-in support for serializing `System.Type` values (nor for using them as dictionary/property keys). Murder needs this for `Dictionary<Type, ...>`-shaped data such as `EntityModifier`'s per-component overrides and blackboard/component type lookups.

**Use-case:** Registered automatically as one of the `Converters` in [MurderSerializerOptionsExtensions.Options](../../Murder/Serialization/MurderSerializerOptionsExtensions.html) — game code never constructs or registers this manually. Simply serializing a field, property, or dictionary key typed as `System.Type` with the Murder serializer options is enough for it to round-trip correctly.

**Implements:** _[JsonConverter\<Type\>](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.JsonConverter-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public JsonTypeConverter()
```

Creates a new converter instance. Has no state of its own; every `Read`/`Write` call resolves the type fresh from the JSON payload or from the `Type` instance being written.

### ⭐ Properties

#### HandleNull

```csharp
public virtual bool HandleNull { get; }
```

Inherited from `JsonConverter<T>` and left at its default (`false`); this converter does not special-case `null` type references, so a `null` `Type` value will fail deserialization rather than being handled explicitly.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Type

```csharp
public virtual Type Type { get; }
```

Inherited from `JsonConverter<T>`; reports the CLR type this converter handles, which is always `System.Type` itself.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

### ⭐ Methods

#### Read(Utf8JsonReader&, Type, JsonSerializerOptions)

```csharp
public override Type Read(ref Utf8JsonReader reader, Type typeToConvert, JsonSerializerOptions options)
```

Resolves the `Type` whose `AssemblyQualifiedName` is the next JSON string token, via `Type.GetType(string)`. Throws a `JsonException` if the string is missing or does not resolve to a loaded type — for example, because the type it referred to was renamed, moved, or deleted since the JSON was written. Deserializing an arbitrary, untrusted assembly-qualified name is generally unsafe; this is acceptable here only because Murder always (de)serializes its own trusted project files, never arbitrary external input.

**Parameters** \
`reader` [Utf8JsonReader&](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonReader?view=net-7.0) \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Exceptions** \
[JsonException](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonException?view=net-7.0) \

#### ReadAsPropertyName(Utf8JsonReader&, Type, JsonSerializerOptions)

```csharp
public override Type ReadAsPropertyName(ref Utf8JsonReader reader, Type typeToConvert, JsonSerializerOptions options)
```

Resolves a `Type` that appears as a JSON object property name — i.e. as a dictionary key, such as in `Dictionary<Type, IComponent>` — rather than as a value. Delegates straight to `Read` using the same assembly-qualified-name format.

**Parameters** \
`reader` [Utf8JsonReader&](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonReader?view=net-7.0) \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### Write(Utf8JsonWriter, Type, JsonSerializerOptions)

```csharp
public override void Write(Utf8JsonWriter writer, Type value, JsonSerializerOptions options)
```

Writes `value` as a JSON string containing its `AssemblyQualifiedName`, so it can later be resolved back to the same `Type` by `Read`.

**Parameters** \
`writer` [Utf8JsonWriter](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonWriter?view=net-7.0) \
`value` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

#### WriteAsPropertyName(Utf8JsonWriter, Type, JsonSerializerOptions)

```csharp
public override void WriteAsPropertyName(Utf8JsonWriter writer, Type value, JsonSerializerOptions options)
```

Writes `value` as a JSON object property name using its assembly-qualified name, for the case where a `Type` is used as a dictionary key. Falls back to an empty-string property name if `value` has no assembly-qualified name (e.g. an open generic type parameter).

**Parameters** \
`writer` [Utf8JsonWriter](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonWriter?view=net-7.0) \
`value` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

⚡

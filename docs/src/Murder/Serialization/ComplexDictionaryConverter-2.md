# ComplexDictionaryConverter\<T, V\>

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public sealed class ComplexDictionaryConverter<T, V> : JsonConverter<ComplexDictionary<T, V>>
```

Custom `JsonConverter<ComplexDictionary<T, V>>` that lets a [ComplexDictionary\<TKey, TValue\>](../../Murder/Serialization/ComplexDictionary-2.html) round-trip through `System.Text.Json` even when `T` is not a `string`/primitive key type.

**Intent:** `System.Text.Json` cannot natively serialize a dictionary whose keys aren't strings (or a small set of primitives it can stringify) — a `ComplexDictionary<Point, Point>` (pathfinding route maps) or `ComplexDictionary<Type, IComponent>` (`Murder.Prefabs.EntityModifier` component overrides) would otherwise throw at serialization time. This converter works around that by writing each entry as its own `"key"`/`"value"` property pair directly on a single JSON object — so the written object ends up with a repeated `"key"`/`"value"` property pair per dictionary entry, rather than the usual one-property-per-entry shape a normal dictionary would produce — and delegating the actual encoding of each key/value to whatever converter is already registered for `T`/`V` in the current `JsonSerializerOptions`.

**Use-case:** Registered automatically — one closed instance per `ComplexDictionary<T, V>` generic actually used in the project — in the `Converters` list of [MurderSerializerOptionsExtensions.Options](../../Murder/Serialization/MurderSerializerOptionsExtensions.html). Game code never constructs or registers this converter directly; simply declaring a field as `ComplexDictionary<T, V>` is enough.

**Implements:** _[JsonConverter\<ComplexDictionary\<T, V\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.JsonConverter-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public ComplexDictionaryConverter<T, V>()
```

Creates a new converter instance. The converter is stateful in one respect — it lazily resolves and caches the `T`/`V` key/value converters on first use (see `InitializeArrayResolver`) — so a single instance should not be shared across `JsonSerializerOptions` with different converter configurations. In practice the source generator creates one instance per `ComplexDictionary<T, V>` closed type, which is safe.

### ⭐ Properties

#### HandleNull

```csharp
public virtual bool HandleNull { get; }
```

Inherited from `JsonConverter<T>` and left at its default (`false`); a `null` `ComplexDictionary<T, V>` reference is not specially handled by this converter.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Type

```csharp
public virtual Type Type { get; }
```

Inherited from `JsonConverter<T>`; reports the closed generic `ComplexDictionary<T, V>` type this particular converter instance handles.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

### ⭐ Methods

#### CanConvert(Type)

```csharp
public virtual bool CanConvert(Type typeToConvert)
```

Returns `true` if `typeToConvert` is the `ComplexDictionary<T, V>` closed generic this converter was created for.

**Parameters** \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Read(Utf8JsonReader&, Type, JsonSerializerOptions)

```csharp
public override ComplexDictionary<T, V>? Read(ref Utf8JsonReader reader, Type typeToConvert, JsonSerializerOptions options)
```

Deserializes a `ComplexDictionary<T, V>` by reading the repeated `"key"`/`"value"` property pairs written by `Write`, decoding each key with `T`'s own registered `JsonConverter<T>` and each value with `V`'s. Throws `InvalidOperationException` if no converter can be resolved for `T` or `V`, or `JsonException` if a key or value reads back as `null`.

**Parameters** \
`reader` [Utf8JsonReader&](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonReader?view=net-7.0) \
`typeToConvert` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

**Returns** \
[ComplexDictionary\<T, V\>](../../Murder/Serialization/ComplexDictionary-2.html) \

**Exceptions** \
[InvalidOperationException](https://learn.microsoft.com/en-us/dotnet/api/System.InvalidOperationException?view=net-7.0), [JsonException](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonException?view=net-7.0) \

#### Write(Utf8JsonWriter, ComplexDictionary<T, V>, JsonSerializerOptions)

```csharp
public override void Write(Utf8JsonWriter writer, ComplexDictionary<T, V> dictionary, JsonSerializerOptions options)
```

Serializes `dictionary` to JSON by writing every entry as its own `"key"`/`"value"` property pair on a single JSON object, in the format expected by `Read`.

**Parameters** \
`writer` [Utf8JsonWriter](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Utf8JsonWriter?view=net-7.0) \
`dictionary` [ComplexDictionary\<T, V\>](../../Murder/Serialization/ComplexDictionary-2.html) \
`options` [JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

⚡

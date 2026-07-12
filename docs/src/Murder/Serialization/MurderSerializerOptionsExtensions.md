# MurderSerializerOptionsExtensions

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public static class MurderSerializerOptionsExtensions
```

Source-generated (by the `Murder.Serializer` Roslyn generator, from a template keyed on the compiling project's assembly name — `Murder` for the engine itself) static class that exposes the single, fully-configured `JsonSerializerOptions` instance used for every JSON (de)serialization in the engine.

**Intent:** Assemble, once, all of the pieces `System.Text.Json` needs to (de)serialize Murder's component/asset/interaction graph without reflection: the source-generated `TypeInfoResolver` ([MurderSourceGenerationContext](../../Murder/Serialization/MurderSourceGenerationContext.html)), a modifier that pulls in private `[Serialize]`/`[ShowInEditor]` fields via `SerializationHelper.ApplyModifierForPrivateFieldsAndGetters`, polymorphic-type metadata for interfaces like `IComponent`/`IInteraction` (so a field typed as an interface can deserialize back to its concrete derived type), and the custom converters ([ComplexDictionaryConverter\<T, V\>](../../Murder/Serialization/ComplexDictionaryConverter-2.html) per closed `ComplexDictionary<T, V>`, plus [JsonTypeConverter](../../Murder/Serialization/JsonTypeConverter.html)).

**Use-case:** Reference `MurderSerializerOptionsExtensions.Options` (rarely directly — most code instead goes through `Game.Data.SerializationOptions`, which falls back to it, or through [FileManager](../../Murder/Serialization/FileManager.html)'s `SerializeToJson`/`DeserializeFromJson` helpers, which already use it) wherever you need to serialize or deserialize Murder types with `System.Text.Json` outside of those helpers.

### ⭐ Properties

#### Options

```csharp
public static readonly JsonSerializerOptions Options;
```

The default, pre-built `JsonSerializerOptions` that should be used when serializing or deserializing any component, asset, or other project type. Configured with `PreferredObjectCreationHandling = Replace`, `IncludeFields = true`, `WriteIndented = true`, `IgnoreReadOnlyFields = false`, `IgnoreReadOnlyProperties = true`, `PropertyNameCaseInsensitive = true`, and `DefaultIgnoreCondition = WhenWritingNull` — settings chosen to match how Murder's readonly-struct components and record-style assets are shaped, and to keep saved JSON diffable/human-readable. If a downstream game project also runs the `Murder.Serializer` generator, its own `{ProjectName}SerializerOptionsExtensions.Options` combines this engine-level resolver with the game's own via `JsonTypeInfoResolver.Combine`, so both sets of types resolve from a single options instance.

**Returns** \
[JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

⚡

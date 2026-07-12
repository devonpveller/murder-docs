# SerializationHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class SerializationHelper
```

Utilities that customize how Murder's `System.Text.Json`-based save/asset serialization treats private fields, getter-only properties, and deep-copying of already-serializable objects.

**Intent:** This is the glue that lets the engine keep its data types as immutable, private-backing-field readonly structs while still persisting and cloning them correctly.

**Use-case:** Use `DeepCopy<T>` to clone components or assets (notably in the editor, where a fresh copy is required so edits don't mutate shared memory), `WithModifiers` to compose a `JsonTypeInfoResolver` with additional customizations, and `ApplyModifierForPrivateFieldsAndGetters` (registered via `WithModifiers`) to make private, `[Serialize]`/`[ShowInEditor]`-attributed fields participate in JSON serialization.

### ⭐ Methods

#### WithModifiers(IJsonTypeInfoResolver, Action\`1[])

```csharp
public IJsonTypeInfoResolver WithModifiers(IJsonTypeInfoResolver resolver, Action`1[] modifiers)
```

Wraps an existing `IJsonTypeInfoResolver` so that every `JsonTypeInfo` it produces is additionally passed through `modifiers` before use. This is the standard System.Text.Json pattern for composing serialization customizations (e.g. chaining `ApplyModifierForPrivateFieldsAndGetters` together with source-generated resolvers) without subclassing the resolver.

**Parameters** \
`resolver` [IJsonTypeInfoResolver](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.Metadata.IJsonTypeInfoResolver?view=net-7.0) — The base resolver to wrap. \
`modifiers` [Action\<T\>[]](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) — Delegates invoked, in order, on each resolved `JsonTypeInfo`. \

**Returns** \
[IJsonTypeInfoResolver](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.Metadata.IJsonTypeInfoResolver?view=net-7.0) — A new resolver that applies `modifiers` on top of `resolver`'s output. \

#### DeepCopy(T)

```csharp
public T DeepCopy(T c)
```

Creates a deep copy of the given object by serializing it to JSON (via `Game.Data.SerializationOptions`) and deserializing a fresh instance. This is deliberately roundabout: Murder's components are readonly structs for performance, so there is no cheap generic "clone" available, and the editor needs a genuinely independent copy so edits to one entity's component don't alias the memory of another entity using the same struct value. Throws `InvalidOperationException` if deserialization somehow fails to produce a `T`.

**Parameters** \
`c` [T](../../) \

**Returns** \
[T](../../) \

#### ApplyModifierForPrivateFieldsAndGetters(JsonTypeInfo)

```csharp
public void ApplyModifierForPrivateFieldsAndGetters(JsonTypeInfo jsonTypeInfo)
```

A `System.Text.Json` type-info modifier (meant to be registered via `WithModifiers`) that makes private/serialize-attributed fields and getter-only properties on Murder types (components, assets) participate in JSON serialization even though the source generator normally only sees public members with both a getter and setter. It removes properties that can't actually be written back (no setter, no matching constructor parameter, not explicitly opted in), and adds reflection-backed accessors for private fields marked with `[Serialize]` or `[ShowInEditor]`, walking up the type's base classes so inherited private fields are picked up too. This is what allows the engine's readonly-struct components (which favor private backing fields) to still round-trip through JSON in save files and asset files.

**Parameters** \
`jsonTypeInfo` [JsonTypeInfo](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.Metadata.JsonTypeInfo?view=net-7.0) — The type info being built by the serializer for a given type; mutated in place. \

⚡

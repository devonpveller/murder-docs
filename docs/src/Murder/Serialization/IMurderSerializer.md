# IMurderSerializer

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public interface IMurderSerializer
```

An empty marker interface implemented by every source-generated `JsonSerializerContext` that the `Murder.Serializer` Roslyn generator emits — [MurderSourceGenerationContext](../../Murder/Serialization/MurderSourceGenerationContext.html) for the Murder engine itself, and an equivalent `{ProjectName}SourceGenerationContext` generated inside each downstream game project.

**Intent:** Give the source generator a stable, well-known type it can look up by fully-qualified name (`Murder.Serialization.IMurderSerializer`) via Roslyn's `Compilation.GetTypeByMetadataName`, without depending on any particular context class name.

**Use-case:** When a game project is compiled, `Murder.Serializer` scans the assemblies it references (starting with `Murder.dll`) for the first class that implements `IMurderSerializer` and treats it as the "parent" serialization context. The game's own generated `{ProjectName}SerializerOptionsExtensions.Options` then combines its `IJsonTypeInfoResolver` with that parent's, via `JsonTypeInfoResolver.Combine`, instead of duplicating type metadata for every type already known to Murder. You should never implement this interface directly in game code — it only ever appears on generator output.

⚡

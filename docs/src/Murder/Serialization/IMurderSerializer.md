# IMurderSerializer

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public abstract IMurderSerializer
```

Marker interface implemented by JSON source-generation contexts that provide type metadata for Murder's serialization pipeline.

**Intent:** Identifies serialization context classes so the engine can discover and combine multiple JSON type info resolvers at runtime.

**Use-case:** Implement in a `JsonSerializerContext` subclass (alongside `[JsonSerializable]` attributes) and register it with the Murder serializer options to extend serialization support for game-specific types.



⚡
# SoundParameterComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundParameterComponent : IComponent
```

Marker component that indicates this entity carries runtime sound parameter data used by the audio system.

**Intent:** Tag an entity as a source of sound parameter overrides so the audio system can locate and apply them.

**Use-case:** Attach alongside sound-related components to inform the audio pipeline that additional parameter data is available on this entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡
# IndestructibleComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct IndestructibleComponent : IComponent
```

Component used when an entity will no longer receive any
            damage from a hit.

**Intent:** Mark an entity as immune to destruction so that damage and destruction systems skip it entirely.

**Use-case:** Add to boss entities during scripted invincibility phases, or to critical world objects (e.g. save points) that must never be destroyed during normal gameplay.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡
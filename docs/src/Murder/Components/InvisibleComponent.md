# InvisibleComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InvisibleComponent : IComponent
```

All render systems are supposed to filter out this component

**Intent:** Mark an entity as invisible so that all render systems skip drawing it.

**Use-case:** Add to an entity that should temporarily or permanently be hidden (e.g. a trigger area, a logic entity, or during a fade-out); remove the component to make the entity visible again.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

⚡

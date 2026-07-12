# DisableEntityComponent

**Namespace:** Murder.Components.Effects \
**Assembly:** Murder.dll

```csharp
public sealed struct DisableEntityComponent : IComponent
```

Marker component that temporarily excludes this entity from world queries that explicitly filter it out.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Unlike [Entity](../../../Bang/Entities/Entity.html)'s built-in `Deactivate`, this is a plain opt-in component: it only has an effect on systems that explicitly exclude it via a `NoneOf` filter. `StaticRenderQuadTreeSystem`, for example, filters out any entity carrying this component so it is skipped when the static render quad-tree is built and rebuilt. This gives individual systems a lightweight way to treat an entity as "not really there" without engaging the full deactivation machinery.

**Use-case:** Attach to temporarily hide an entity from the specific systems that check for it (e.g. a chest that has already been opened, or scenery that shouldn't be considered part of the world yet) without destroying it. Remove the component to make the entity visible to those systems again. This component is decorated with `[DoNotPersistOnSave]`, so it represents transient runtime state and is not written out when the world is saved.

⚡

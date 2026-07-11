# IDoNotCheckOnReplaceTag

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public interface IDoNotCheckOnReplaceTag
```

This will tag a component such that it should not do an equals operation
            prior to replacing it.

By default, `Entity.ReplaceComponent<T>(...)` short-circuits when the incoming value is equal to
the component already on the entity (via [IComponent.Equals](../../Bang/Components/IComponent.html)),
skipping the replace and all of its notifications entirely — this is a performance optimization to
avoid redundant `OnComponentModified` churn when a system replaces a component with the same value
every frame. Implementing `IDoNotCheckOnReplaceTag` on a component opts it out of that equality
check, so a replace always goes through (unless `forceReplace` is already implied). The same tag is
also checked by `Entity`'s post-replace notification step, where it suppresses the "further
notifications" pass (context/child notifications) for that component even when the replace does go
through — in other words, this tag marks a component as one whose replaces should always be applied
but should not be treated as a semantically meaningful "value changed" event by observers.

Use this for components whose equality is either meaningless or expensive to compute correctly,
or that are replaced purely to refresh some derived/cached state rather than to signal a change —
for example `RenderedSpriteCacheComponent`
(`src\Murder\Components\Graphics\RenderedSpriteCacheComponent.cs`), which combines
`IComponent`, [IModifiableComponent](../../Bang/Components/IModifiableComponent.html), and
`IDoNotCheckOnReplaceTag` together since it exists purely as a rendering cache that gets
overwritten frequently and should never block on an equality check.



⚡
# IComponent

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public abstract IComponent
```

A set of components will define an entity. This can be any sort of game abstraction.
            Bang follows the convention of only defining components for readonly structs.

`IComponent` is the marker interface at the root of Bang's ECS: every piece of data attached to an
[Entity](../../Bang/Entities/Entity.html) — position, sprite, velocity, AI state, and so on — is a
type that implements this interface, and an entity is nothing more than an id plus the bag of
components attached to it. The interface itself declares no instance members; its only member is a
static helper, `Equals(IComponent?, IComponent?)`, used internally by the engine (for example when
[Entity.ReplaceComponent](../../Bang/Entities/Entity.html) decides whether a replace actually
changes the component's value) to compare two components for equality while treating two nulls as
equal.

By convention — and this matters, because the engine relies on component instances being cheap to
copy and safe to compare by value — components should be declared as `readonly struct` types, not
classes. A typical component in the Murder engine looks like `public readonly struct
SkipComponent : IComponent { }` (see
`src\Murder\Components\World\SkipComponent.cs`) for a pure "tag" component with no data, or a
struct with `readonly` fields/properties for components that carry data (e.g.
[PositionComponent](../../Bang/Components/PositionComponent.html)). If a component needs to be
mutated in place and have subscribers notified of the change, it should instead implement
[IModifiableComponent](../../Bang/Components/IModifiableComponent.html) in addition to
`IComponent`. Game code and tools (including autonomous agents generating new gameplay data)
should implement `IComponent` directly on any new readonly struct that represents a piece of
entity state, and add it to an entity via `Entity.AddComponent`/`Entity.SetComponent`.



⚡
# KeepOnReplaceAttribute

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public class KeepOnReplaceAttribute : Attribute
```

Marks components that must be kept on an entity
            [Entity.Replace(Bang.Components.IComponent[],System.Collections.Generic.List{System.ValueTuple{System.Int32,System.String}},System.Boolean)](../../Bang/Entities/Entity.html#replace(icomponent[],) operation.

`Entity.Replace(...)` is used to swap the entire set of components/children on an existing entity
for a new set — typically when re-instantiating an entity from a prefab/instance after it was
edited (e.g. in the level editor), or when reloading saved data. When called with `wipe: true`, any
component the entity currently has that is *not* part of the incoming replacement set is normally
removed. Tagging a component's type with `[KeepOnReplace]` opts it out of that wipe: the component
survives the replace untouched even though it wasn't included in the new component list, and if it
*is* included in the new list it is still force-replaced rather than skipped. Use this attribute
for components that hold identity or transient runtime state that must not be reset just because
the entity's authored data changed — for example `FacingComponent`
(`src\Murder\Components\Agents\FacingComponent.cs`), `IgnoreUntilComponent`
(`src\Murder\Components\Utilities\IgnoreUntilComponent.cs`), and the `IdTargetComponent`/
`IdTargetCollectionComponent` pair used to preserve entity-id references across a replace
(`src\Murder\Components\Serialization\IdTargetComponent.cs`,
`IdTargetCollectionComponent.cs`). Without this attribute, any runtime-computed component not
present in the freshly-authored data would silently disappear the next time the entity is
replaced.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public KeepOnReplaceAttribute()
```

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
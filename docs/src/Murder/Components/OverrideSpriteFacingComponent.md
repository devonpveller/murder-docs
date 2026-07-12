# OverrideSpriteFacingComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct OverrideSpriteFacingComponent : IComponent
```

Runtime, dictionary-backed set of [SpriteFacingComponent](../../Murder/Components/SpriteFacingComponent.html) overrides, keyed by prefix id.

**Intent:** Built from [OverrideSpriteFacingEditorComponent](../../Murder/Components/OverrideSpriteFacingEditorComponent.html) by [EntityBuilder](../../Murder/Prefabs/EntityBuilder.html) when an entity is instantiated. `DirectionHelper.GetSuffixFromAngle` checks this component first (looking up `Faces` by the caller-supplied prefix) before falling back to the entity's plain `SpriteFacingComponent`, letting a single entity expose different facing/suffix behavior for different sprite parts (e.g. body vs. weapon) keyed by prefix. Runtime-only, persisted on save, and hidden from the editor's component picker since it is generated rather than hand-authored.

**Use-case:** Read via `entity.TryGetOverrideSpriteFacing()` (typically indirectly, through `DirectionHelper.GetSuffixFromAngle`) rather than constructed directly by gameplay code — it is produced automatically from an entity's authored [OverrideSpriteFacingEditorComponent](../../Murder/Components/OverrideSpriteFacingEditorComponent.html) when the prefab is built.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public OverrideSpriteFacingComponent()
```

Creates an override set with no entries.

```csharp
public OverrideSpriteFacingComponent(ImmutableDictionary<string, SpriteFacingComponent> faces)
```

**Parameters** \
`faces` [ImmutableDictionary\<string, SpriteFacingComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

### ⭐ Properties

#### Faces

```csharp
public readonly ImmutableDictionary<string, SpriteFacingComponent> Faces;
```

Facing overrides keyed by prefix id, checked by `DirectionHelper.GetSuffixFromAngle` before the entity's default [SpriteFacingComponent](../../Murder/Components/SpriteFacingComponent.html).

**Returns** \
[ImmutableDictionary\<string, SpriteFacingComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

⚡

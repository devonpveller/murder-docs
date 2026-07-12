# OverrideSpriteFacingEditorComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct OverrideSpriteFacingEditorComponent : IComponent
```

Editor-authored (design-time) list of [SpriteFacingComponent](../../Murder/Components/SpriteFacingComponent.html) overrides, keyed by id.

**Intent:** This is the shape an author edits directly on a prefab in the level editor. At build/instantiation time, [EntityBuilder](../../Murder/Prefabs/EntityBuilder.html) reads `SpriteFaces`, converts it into an `ImmutableDictionary<string, SpriteFacingComponent>`, calls `entity.SetOverrideSpriteFacing(...)` with it (producing the runtime [OverrideSpriteFacingComponent](../../Murder/Components/OverrideSpriteFacingComponent.html)), and removes this editor-only component — so it never exists on a fully-built entity at runtime.

**Use-case:** Add to a prefab in the editor when an entity needs different `SpriteFacingComponent` behavior for different sprite parts, each keyed by a prefix id (see [SpriteFacingId](../../Murder/Components/SpriteFacingId.html)). Do not expect this component to be present at runtime; read [OverrideSpriteFacingComponent](../../Murder/Components/OverrideSpriteFacingComponent.html) instead from gameplay/render code.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public OverrideSpriteFacingEditorComponent()
```

Creates an empty override list.

### ⭐ Properties

#### SpriteFaces

```csharp
public readonly ImmutableArray<SpriteFacingId> SpriteFaces;
```

The authored list of id-to-facing overrides, later converted into [OverrideSpriteFacingComponent](../../Murder/Components/OverrideSpriteFacingComponent.html).`Faces` by [EntityBuilder](../../Murder/Prefabs/EntityBuilder.html).

**Returns** \
[ImmutableArray\<SpriteFacingId\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡

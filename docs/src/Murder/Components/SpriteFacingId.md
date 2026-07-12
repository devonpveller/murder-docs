# SpriteFacingId

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteFacingId
```

One editor-authored entry pairing an identifier with a [SpriteFacingComponent](../../Murder/Components/SpriteFacingComponent.html) override.

**Intent:** Used exclusively inside [OverrideSpriteFacingEditorComponent](../../Murder/Components/OverrideSpriteFacingEditorComponent.html).`SpriteFaces` to build a keyed list of per-prefix facing overrides. [EntityBuilder](../../Murder/Prefabs/EntityBuilder.html) converts the authored array into the `ImmutableDictionary<string, SpriteFacingComponent>` stored on the runtime [OverrideSpriteFacingComponent](../../Murder/Components/OverrideSpriteFacingComponent.html), keyed by `Id`.

**Use-case:** Authored as part of `OverrideSpriteFacingEditorComponent.SpriteFaces` in the level editor, one entry per prefix that needs its own facing behavior (e.g. a character's body vs. a held weapon sprite facing differently). `Id` should match the `prefix` argument later passed to `DirectionHelper.GetSuffixFromAngle` for the override to be picked up.

### ⭐ Constructors

```csharp
public SpriteFacingId()
```

Creates an empty facing override entry (empty `Id`, default `Info`).

### ⭐ Properties

#### Id

```csharp
public readonly string Id;
```

The lookup key (typically a facing/prefix name) that identifies this override, matched against the `prefix` passed to `DirectionHelper.GetSuffixFromAngle`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Info

```csharp
public readonly SpriteFacingComponent Info;
```

The facing configuration to use for entities/prefixes matching `Id`.

**Returns** \
[SpriteFacingComponent](../../Murder/Components/SpriteFacingComponent.html) \

⚡

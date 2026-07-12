# Tags

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct Tags
```

A compact bitmask value used to assign and match against one or more integer tag bits, such as the constants defined by a game-specific subclass of `MurderTagsBase`.

**Intent:** Used both as an entity-side "which tags do I have" value (via `TagsComponent`) and as a filter-side "which tags do I care about" value (e.g. `MovementModAreaComponent.AffectOnly`), with `All` controlling whether the filter requires an actual bit match or treats the default (no explicit flags) as "match everything".

**Use-case:** Leave a `Tags` field at its default (`new Tags()`) to mean "applies to everything, no filtering" — for example, a `MovementModAreaComponent` with a default `AffectOnly` slows down every agent that overlaps it. Construct with `Tags(flags)` or `Tags(flags, all)` to restrict a filter to entities/agents that carry specific tag bits.

### ⭐ Constructors

```csharp
public Tags()
```

Creates a wildcard `Tags` that matches everything (`All` is `true`, no flags set). This is the default/blank state used by the editor and serializer.

```csharp
public Tags(int flags, bool all)
```

Creates a `Tags` with an explicit bitmask and match mode.

**Parameters** \
`flags` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`all` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public Tags(int flags)
```

Creates a `Tags` restricted to the given bitmask (`All` is set to `false`), so `HasTag` only matches when at least one bit of `flags` overlaps.

**Parameters** \
`flags` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### All

```csharp
public readonly bool All;
```

When `true` (the default, produced by the parameterless constructor), this value is treated as an unconditional match regardless of `Flags` — i.e. "no filtering, match everything". Set to `false` (via `Tags(int)` or `Tags(int, bool)`) to require that at least one of the bits in `Flags` actually be present.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Flags

```csharp
public readonly int Flags;
```

The bitmask of tag bits carried or matched by this value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### HasTag(int)

```csharp
public bool HasTag(int tag)
```

Checks whether this `Tags` matches `tag`: always `true` when `All` is set, otherwise `true` when `tag` shares at least one bit with `Flags`.

**Parameters** \
`tag` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasTags(Tags)

```csharp
public bool HasTags(Tags tags)
```

Checks whether this `Tags` matches the flags carried by `tags`, applying this value's own `All` semantics.

**Parameters** \
`tags` [Tags](../../Murder/Core/Tags.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡

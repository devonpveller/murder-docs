# Tags

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct Tags
```

A bitmask struct used to assign and match entity tags defined in `MurderTagsBase`.

**Intent:** Compact representation of one or more entity tags, with a flag to control whether all bits must match or any single bit suffices.

**Use-case:** Assign to the `TagsComponent` on an entity, or pass to query helpers that filter entities by tag.

### ⭐ Constructors
```csharp
public Tags()
```

Creates an empty `Tags` value with no flags set.

```csharp
public Tags(int flags, bool all)
```

Creates a `Tags` value with the given flag bitmask and match mode.

**Parameters** \
`flags` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`all` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public Tags(int flags)
```

Creates a `Tags` value from the given flag bitmask (match-any mode).

**Parameters** \
`flags` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### All
```csharp
public readonly bool All;
```

When `true`, all bits in `Flags` must be present for a match; when `false`, any matching bit suffices.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Flags
```csharp
public readonly int Flags;
```

The bitmask of tag bits assigned to this `Tags` value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### HasTag(int)
```csharp
public bool HasTag(int tag)
```

Returns `true` when the given `tag` bit is set in this `Tags` value.

**Parameters** \
`tag` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasTags(Tags)
```csharp
public bool HasTags(Tags tags)
```

Returns `true` when this value satisfies the conditions in `tags`, taking into account the `All` flag.

**Parameters** \
`tags` [Tags](../../Murder/Core/Tags.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \



⚡
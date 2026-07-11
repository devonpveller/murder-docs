# MurderTransformExtensions

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public static class MurderTransformExtensions
```

Extension methods for querying and modifying the `IMurderTransformComponent` on any entity.

**Intent:** Provide a convenient API for getting, setting, and checking transform components without knowing which concrete transform type is attached to an entity.

**Use-case:** Call `e.GetMurderTransform()` in any system to retrieve the entity's transform, or `e.SetMurderTransform(t)` to update it, regardless of whether the entity uses `PositionComponent` or a custom transform.

### ⭐ Methods
#### HasMurderTransform(Entity)
```csharp
public bool HasMurderTransform(Entity e)
```

Returns `true` if the entity currently has an `IMurderTransformComponent` attached.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveMurderTransform(Entity)
```csharp
public bool RemoveMurderTransform(Entity e)
```

Removes the `IMurderTransformComponent` from the entity if it exists and returns `true` on success.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetMurderTransform(Entity)
```csharp
public IMurderTransformComponent GetMurderTransform(Entity e)
```

Retrieves the entity's `IMurderTransformComponent`, throwing if none is present.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### TryGetMurderTransform(Entity)
```csharp
public IMurderTransformComponent TryGetMurderTransform(Entity e)
```

Attempts to retrieve the entity's `IMurderTransformComponent`, returning `null` if none is present.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### SetMurderTransform(Entity, IMurderTransformComponent)
```csharp
public void SetMurderTransform(Entity e, IMurderTransformComponent component)
```

Sets or replaces the entity's `IMurderTransformComponent` with the provided value.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`component` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \



⚡
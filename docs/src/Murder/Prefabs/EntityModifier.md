# EntityModifier

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public class EntityModifier
```

Records the component additions, removals, and child-instance overrides that a `PrefabEntityInstance` applies on top of its parent prefab.

**Intent:** Encapsulates all customizations that distinguish one placed prefab instance from the base `PrefabAsset` definition.

**Use-case:** Created and manipulated by `PrefabEntityInstance` and the editor; game code rarely constructs these directly.

### ⭐ Constructors
```csharp
public EntityModifier(Guid guid)
```
Creates a new empty modifier for the entity identified by `guid`.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### Children
```csharp
public ImmutableArray<T> Children { get; }
```
Immutable set of child entity GUIDs that this modifier adds to the parent instance.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Guid
```csharp
public readonly Guid Guid;
```
The GUID of the entity this modifier is associated with.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
### ⭐ Methods
#### HasChild(Guid)
```csharp
public bool HasChild(Guid childId)
```
Returns `true` if this modifier adds a child entity with the given GUID.

**Parameters** \
`childId` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasComponent(Type)
```csharp
public bool HasComponent(Type t)
```
Returns `true` if this modifier adds or overrides a component of the given type.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsComponentRemoved(Type)
```csharp
public bool IsComponentRemoved(Type t)
```
Returns `true` if this modifier explicitly removes the component of the given type.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetComponent(Type, out IComponent&)
```csharp
public bool TryGetComponent(Type t, IComponent& result)
```
Attempts to retrieve the overriding component of type `t`; returns `true` and writes to `result` if found.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`result` [IComponent&](../../Bang/Components/IComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### UndoCustomComponent(Type)
```csharp
public bool UndoCustomComponent(Type t)
```
Removes the component override of type `t` from this modifier; returns `true` if it was present.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ApplyModifiersFrom(EntityModifier)
```csharp
public EntityModifier ApplyModifiersFrom(EntityModifier other)
```

Merge modifier with <paramref name="other" />.
            This will prioritize items present in <paramref name="other" />.

**Parameters** \
`other` [EntityModifier](../../Murder/Prefabs/EntityModifier.html) \

**Returns** \
[EntityModifier](../../Murder/Prefabs/EntityModifier.html) \

#### FetchChildren()
```csharp
public ImmutableArray<T> FetchChildren()
```
Returns all child entity GUIDs added by this modifier as an immutable array.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FilterComponents(IEnumerable`1&)
```csharp
public ImmutableArray<T> FilterComponents(IEnumerable`1& allComponents)
```
Filters `allComponents` by removing any that this modifier overrides or deletes, and injects the modifier's own component values.

**Parameters** \
`allComponents` [IEnumerable\<T\>&](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### AddChild(EntityInstance)
```csharp
public void AddChild(EntityInstance child)
```
Registers `child` as an entity that this modifier adds to the parent instance.

**Parameters** \
`child` [EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

#### AddOrReplaceComponent(IComponent)
```csharp
public void AddOrReplaceComponent(IComponent c)
```
Adds or replaces the component `c` in this modifier, and removes it from the removal set if present.

**Parameters** \
`c` [IComponent](../../Bang/Components/IComponent.html) \

#### RemoveChild(Guid)
```csharp
public void RemoveChild(Guid guid)
```
Unregisters the child entity with the given GUID from this modifier.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RemoveComponent(Type)
```csharp
public void RemoveComponent(Type t)
```
Marks the component of type `t` for removal, and strips any override value previously added.

**Parameters** \
`t` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \



⚡
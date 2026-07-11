# CutsceneAnchorsEditorComponent

**Namespace:** Murder.Components.Serialization \
**Assembly:** Murder.dll

```csharp
public sealed struct CutsceneAnchorsEditorComponent : IComponent
```

Holds the collection of named anchor points for a cutscene entity, allowing script authors to reference positions by name rather than raw coordinates.

**Intent:** Store all named world-space marks that a cutscene references in one place on the entity.

**Use-case:** Add to an entity that acts as a cutscene container; populate `Anchors` with one [AnchorId](../../../Murder/Components/Serialization/AnchorId.html) per named mark, then reference those names in cutscene scripts or the cutscene editor.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public CutsceneAnchorsEditorComponent()
```

```csharp
public CutsceneAnchorsEditorComponent(ImmutableArray<T> anchors)
```

**Parameters** \
`anchors` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### Anchors
```csharp
public readonly ImmutableArray<T> Anchors;
```

All named anchor points defined for this cutscene entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### FindAnchor(string)
```csharp
public Anchor FindAnchor(string name)
```

Returns the anchor with the given name, or a default anchor if not found.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Anchor](../../../Murder/Core/Cutscenes/Anchor.html) \

#### AddAnchorAt(Vector2)
```csharp
public CutsceneAnchorsEditorComponent AddAnchorAt(Vector2 newPosition)
```

Creates and appends a new anchor at the given world-space position.

**Parameters** \
`newPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[CutsceneAnchorsEditorComponent](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html) \

#### WithAnchorAt(string, Vector2)
```csharp
public CutsceneAnchorsEditorComponent WithAnchorAt(string name, Vector2 newPosition)
```

Returns a new component with the named anchor moved to `newPosition`.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`newPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[CutsceneAnchorsEditorComponent](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html) \

#### WithoutAnchorAt(string)
```csharp
public CutsceneAnchorsEditorComponent WithoutAnchorAt(string name)
```

Returns a new component with the named anchor removed from the list.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[CutsceneAnchorsEditorComponent](../../../Murder/Components/Serialization/CutsceneAnchorsEditorComponent.html) \



⚡
# CutsceneAnchorsComponent

**Namespace:** Murder.Components.Cutscenes \
**Assembly:** Murder.dll

```csharp
public sealed struct CutsceneAnchorsComponent : IComponent
```

This is a list of anchor points of cutscene.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Stores named anchor points used by a cutscene to position entities or cameras at authored locations.

**Use-case:** Attach to a cutscene entity; the cutscene system reads `Anchors` to look up world-space positions by name when executing camera moves or entity teleport actions.

### ⭐ Constructors
```csharp
public CutsceneAnchorsComponent()
```

```csharp
public CutsceneAnchorsComponent(ImmutableDictionary<TKey, TValue> anchors)
```

Creates the component pre-populated with the given named anchor dictionary.

**Parameters** \
`anchors` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

### ⭐ Properties
#### Anchors
```csharp
public readonly ImmutableDictionary<TKey, TValue> Anchors;
```

Map of anchor name to world-space position used during cutscene playback.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \


⚡
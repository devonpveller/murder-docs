# StoryAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class StoryAttribute : Attribute
```

Marks an [IComponent](../../../Bang/Components/IComponent.html) struct as belonging to the "story" system: rule and cutscene-driven interactions that react to the game's blackboard/dialogue state.

**Intent:** Lets the world editor group and surface every entity driven by story rules under a dedicated "Story Entities" view, regardless of which gameplay group it also belongs to.

**Use-case:** Apply to a rule/cutscene-driven interaction component such as `InteractOnRuleMatchComponent`, `InteractOnRuleMatchCollectionComponent`, `InteractOnStartComponent`, or `PickEntityToAddOnStartComponent`. `StoryEditorSystem` and `WorldAssetEditor_Story.DrawStoryEntities` look for components tagged with this attribute (via `ReflectionHelper.FetchComponentsWithAttribute`) to populate the editor's Story tab.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public StoryAttribute()
```

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡

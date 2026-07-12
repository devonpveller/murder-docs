# SoundAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class SoundAttribute : Attribute
```

Marks an [IComponent](../../../Bang/Components/IComponent.html) struct/class as carrying sound-related data.

**Intent:** Lets the world editor group and surface every entity that plays or reacts to audio under a dedicated "Sounds" tab, regardless of which gameplay group it also belongs to.

**Use-case:** Apply to a component that plays or reacts to sound, such as `SoundComponent` (one-shot sound), `AmbienceComponent` (ambience loop), `SoundParameterComponent`, or `SoundShapeComponent`. `EditorSoundServices.GetSoundEntities` scans the world for components tagged with this attribute (via `ReflectionHelper.FetchComponentsWithAttribute`) so `WorldAssetEditor_Sounds` can list and filter those entities in the editor's Sounds tab.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public SoundAttribute()
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

# FolderAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class FolderAttribute : Attribute
```

Marks a field so the editor's inspector draws it as a collapsible "folder" row instead of a plain labeled value.

**Intent:** Lets a large or rarely-edited field (typically a collection) be tucked away behind a fold/unfold toggle so it doesn't clutter the inspector by default.

**Use-case:** Apply to a field such as an events array on an asset (see `SpeakerEventsAsset`'s emotes field) so `CustomComponent.DrawMemberForTarget` renders its label as a fold/unfold toggle instead of a static text label, remembering whether it is expanded per-field across editor sessions of the same target.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public FolderAttribute()
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

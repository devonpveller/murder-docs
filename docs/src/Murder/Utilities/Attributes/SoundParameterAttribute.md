# SoundParameterAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class SoundParameterAttribute : Attribute
```

Attribute used for IComponent structs that will change according to 
            a "story". This is used for debugging and filtering in editor.

**Intent:** Marks a field as a sound parameter reference with a specified parameter scope.

**Use-case:** Apply to a field in a component so the editor shows a sound parameter picker filtered by the given `SoundParameterKind` (local, global, or all).

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public SoundParameterAttribute(SoundParameterKind kind)
```

Creates the attribute specifying the kind of sound parameter the field references.

**Parameters** \
`kind` [SoundParameterKind](../../../Murder/Utilities/Attributes/SoundParameterKind.html) \

### ⭐ Properties
#### Kind
```csharp
public readonly SoundParameterKind Kind;
```

The scope of sound parameters this field references (local, global, or all).

**Returns** \
[SoundParameterKind](../../../Murder/Utilities/Attributes/SoundParameterKind.html) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
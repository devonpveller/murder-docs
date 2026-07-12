# SoundParameterAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class SoundParameterAttribute : Attribute
```

Marks a `string` field as a reference to a named sound/audio-middleware parameter.

**Intent:** Reduces the chance of a mistyped audio parameter name silently doing nothing at runtime, by letting the editor offer a picker instead of a free-text field.

**Use-case:** Apply to a `string` field that names an audio-middleware parameter (as opposed to [ParameterId](../../../Murder/Core/Sounds/ParameterId.html), which is a Guid-based reference resolved through its own custom editor field), and pass a [SoundParameterKind](../../../Murder/Utilities/Attributes/SoundParameterKind.html) to scope which parameters the editor offers: parameters local to a single sound event, parameters shared globally, or both.

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

The scope of sound parameters this field references (local, global, or all); controls which parameters the editor's picker offers.

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

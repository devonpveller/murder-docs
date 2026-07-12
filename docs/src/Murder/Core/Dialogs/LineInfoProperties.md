# LineInfoProperties

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed enum LineInfoProperties : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Bit flags describing editor-authored overrides to how a single dialogue line behaves when played, stored on `LineInfo.Flags`.

**Intent:** Lets a writer toggle small per-line runtime behaviors from the dialogue editor without needing a full `DialogAction`, currently limited to suppressing the automatic portrait sound.

**Use-case:** Read via `LineInfo.Flags`; `CharacterRuntime` checks `SkipDefaultPortraitSound` before playing a portrait's built-in sound for the active line, letting a writer silence it for a specific line.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### None

```csharp
public static const LineInfoProperties None;
```

No overrides; the line behaves with its default, engine-computed behavior.

**Returns** \
[LineInfoProperties](../../../Murder/Core/Dialogs/LineInfoProperties.html) \

#### SkipDefaultPortraitSound

```csharp
public static const LineInfoProperties SkipDefaultPortraitSound;
```

Suppresses the automatic sound normally played from the speaking portrait's sound info when this line plays.

**Returns** \
[LineInfoProperties](../../../Murder/Core/Dialogs/LineInfoProperties.html) \

⚡

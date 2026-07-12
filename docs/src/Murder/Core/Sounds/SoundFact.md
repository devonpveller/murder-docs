# SoundFact

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundFact : IComparable<T>, IEquatable<T>
```

A named key (optionally scoped to a specific blackboard) identifying an integer fact on the save's `BlackboardTracker`, used specifically for sound-driven blackboard writes.

**Intent:** Identify which blackboard field a `SoundRuleAction` should write to, without requiring the caller to know the blackboard system's own fact-lookup API.

**Use-case:** A `SoundRuleAction` embeds a `SoundFact` to say which blackboard field it targets; `SetSoundParameterOnInteraction.Interact` reads `action.Fact.Blackboard`/`action.Fact.Name` and forwards them to `MurderSaveServices.CreateOrGetSave().BlackboardTracker.SetInt`/`SetValue`. In the editor, `SoundFactField` presents a searchable picker (`SearchBox.SearchSoundFacts`) so designers can wire up a `SoundRuleAction` to an existing blackboard fact without typing its name by hand.

**Implements:** _[IComparable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable-1?view=net-7.0), [IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public SoundFact()
```

Creates an empty `SoundFact` (default blackboard, empty name).

```csharp
public SoundFact(string? blackboard, string name)
```

Creates a `SoundFact` identifying `name` within `blackboard`.

**Parameters** \
`blackboard` [string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
The blackboard to look the fact up in; if null, the default blackboard is used. \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
The name of the fact within its blackboard.

### ⭐ Properties

#### Blackboard

```csharp
public readonly string? Blackboard;
```

If null, grab the default blackboard.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Name

```csharp
public readonly string Name;
```

The name of the fact within its blackboard.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### Equals(SoundFact)

```csharp
public virtual bool Equals(SoundFact other)
```

**Parameters** \
`other` [SoundFact](../../../Murder/Core/Sounds/SoundFact.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Object)

```csharp
public virtual bool Equals(Object obj)
```

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CompareTo(SoundFact)

```csharp
public virtual int CompareTo(SoundFact other)
```

**Parameters** \
`other` [SoundFact](../../../Murder/Core/Sounds/SoundFact.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetHashCode()

```csharp
public virtual int GetHashCode()
```

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ToString()

```csharp
public virtual string ToString()
```

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡

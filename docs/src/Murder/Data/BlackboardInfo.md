# BlackboardInfo

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public class BlackboardInfo : IEquatable<T>
```

Holds the runtime type and live instance of a blackboard, pairing the `IBlackboard` object with its CLR type for reflection-based field access.

**Intent:** Bundles together a blackboard's type metadata and its runtime instance so that the `BlackboardTracker` can look up and mutate fields by name.

**Use-case:** Retrieved internally by `BlackboardTracker.FindBlackboard` when evaluating dialogue criteria or setting values; game code typically does not construct these directly.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors
```csharp
protected BlackboardInfo(BlackboardInfo original)
```
Copy constructor that duplicates an existing `BlackboardInfo` record.

**Parameters** \
`original` [BlackboardInfo](../../Murder/Data/BlackboardInfo.html) \

```csharp
public BlackboardInfo(Type Type, IBlackboard Blackboard)
```
Creates a new `BlackboardInfo` with the given CLR type and blackboard instance.

**Parameters** \
`Type` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`Blackboard` [IBlackboard](../../Murder/Core/Dialogs/IBlackboard.html) \

### ⭐ Properties
#### Blackboard
```csharp
public IBlackboard Blackboard { get; public set; }
```
The live blackboard instance that stores the actual variable values.

**Returns** \
[IBlackboard](../../Murder/Core/Dialogs/IBlackboard.html) \
#### EqualityContract
```csharp
protected virtual Type EqualityContract { get; }
```
The concrete type used when comparing two `BlackboardInfo` records for equality.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
#### Type
```csharp
public Type Type { get; public set; }
```
The CLR type of the blackboard class, used for reflection-based field access.

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
### ⭐ Methods
#### PrintMembers(StringBuilder)
```csharp
protected virtual bool PrintMembers(StringBuilder builder)
```
Appends member values to the provided `StringBuilder` for debug output.

**Parameters** \
`builder` [StringBuilder](https://learn.microsoft.com/en-us/dotnet/api/System.Text.StringBuilder?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(BlackboardInfo)
```csharp
public virtual bool Equals(BlackboardInfo other)
```
Returns `true` if `other` has the same `Type` and `Blackboard` reference.

**Parameters** \
`other` [BlackboardInfo](../../Murder/Data/BlackboardInfo.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Object)
```csharp
public virtual bool Equals(Object obj)
```
Returns `true` if `obj` is a `BlackboardInfo` with equivalent field values.

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetHashCode()
```csharp
public virtual int GetHashCode()
```
Returns a hash code derived from `Type` and `Blackboard`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ToString()
```csharp
public virtual string ToString()
```
Returns a human-readable string representation of this instance.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Deconstruct(out Type&, out IBlackboard&)
```csharp
public void Deconstruct(Type& Type, IBlackboard& Blackboard)
```
Deconstructs this instance into its `Type` and `Blackboard` component values.

**Parameters** \
`Type` [Type&](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`Blackboard` [IBlackboard&](../../Murder/Core/Dialogs/IBlackboard.html) \



⚡
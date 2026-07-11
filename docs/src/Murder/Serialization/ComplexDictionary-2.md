# ComplexDictionary\<TKey, TValue\>

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public class ComplexDictionary<TKey, TValue> : Dictionary<TKey, TValue>, IDictionary<TKey, TValue>, ICollection<T>, IEnumerable<T>, IEnumerable, IDictionary, ICollection, IReadOnlyDictionary<TKey, TValue>, IReadOnlyCollection<T>, ISerializable, IDeserializationCallback
```

When serializing dictionaries, System.Text.Json is not able to resolve custom dictionary keys.
            As a workaround for that, we will implement our own complex dictionary converter that manually deserializes
            each key and value.

**Intent:** A serialization-safe dictionary that supports complex (non-string) keys by deferring custom conversion.

**Use-case:** Use wherever a `Dictionary<TKey, TValue>` with non-string keys needs to round-trip through `System.Text.Json` serialization without losing key fidelity.

**Implements:** _[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0), [IDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IDictionary-2?view=net-7.0), [ICollection\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.ICollection-1?view=net-7.0), [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0), [IEnumerable](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.IEnumerable?view=net-7.0), [IDictionary](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.IDictionary?view=net-7.0), [ICollection](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.ICollection?view=net-7.0), [IReadOnlyDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IReadOnlyDictionary-2?view=net-7.0), [IReadOnlyCollection\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IReadOnlyCollection-1?view=net-7.0), [ISerializable](https://learn.microsoft.com/en-us/dotnet/api/System.Runtime.Serialization.ISerializable?view=net-7.0), [IDeserializationCallback](https://learn.microsoft.com/en-us/dotnet/api/System.Runtime.Serialization.IDeserializationCallback?view=net-7.0)_

### ⭐ Constructors
```csharp
public ComplexDictionary<TKey, TValue>()
```

```csharp
public ComplexDictionary<TKey, TValue>(IDictionary<TKey, TValue> dictionary)
```
Creates a `ComplexDictionary` pre-populated from an existing dictionary.

**Parameters** \
`dictionary` [IDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IDictionary-2?view=net-7.0) \

```csharp
public ComplexDictionary<TKey, TValue>(IEqualityComparer<T> comparer)
```
Creates an empty `ComplexDictionary` using the specified equality comparer for keys.

**Parameters** \
`comparer` [IEqualityComparer\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEqualityComparer-1?view=net-7.0) \

### ⭐ Properties
#### Comparer
```csharp
public IEqualityComparer<T> Comparer { get; }
```
The equality comparer used to determine key equality in this dictionary.

**Returns** \
[IEqualityComparer\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEqualityComparer-1?view=net-7.0) \
#### Count
```csharp
public virtual int Count { get; }
```
The number of key-value pairs currently stored in this dictionary.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Item
```csharp
public virtual TValue Item { get; public set; }
```
Gets or sets the value associated with the specified key.

**Returns** \
[TValue](../../) \
#### Keys
```csharp
public KeyCollection<TKey, TValue> Keys { get; }
```
The collection of all keys in this dictionary.

**Returns** \
[KeyCollection\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.KeyCollection-KeyCollection?view=net-7.0) \
#### Values
```csharp
public ValueCollection<TKey, TValue> Values { get; }
```
The collection of all values in this dictionary.

**Returns** \
[ValueCollection\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.ValueCollection-ValueCollection?view=net-7.0) \
### ⭐ Methods
#### ContainsValue(TValue)
```csharp
public bool ContainsValue(TValue value)
```
Returns `true` if any entry in the dictionary has the given value.

**Parameters** \
`value` [TValue](../../) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Remove(TKey, out TValue&)
```csharp
public bool Remove(TKey key, TValue& value)
```
Removes the entry for `key` and writes its value to `value`; returns `true` if found.

**Parameters** \
`key` [TKey](../../) \
`value` [TValue&](../../) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryAdd(TKey, TValue)
```csharp
public bool TryAdd(TKey key, TValue value)
```
Adds the entry only if `key` is not already present; returns `true` if added.

**Parameters** \
`key` [TKey](../../) \
`value` [TValue](../../) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetEnumerator()
```csharp
public Enumerator<TKey, TValue> GetEnumerator()
```
Returns an enumerator that iterates through the key-value pairs in this dictionary.

**Returns** \
[Enumerator\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Enumerator-Enumerator?view=net-7.0) \

#### EnsureCapacity(int)
```csharp
public int EnsureCapacity(int capacity)
```
Ensures the dictionary can hold at least `capacity` entries without resizing; returns the actual capacity.

**Parameters** \
`capacity` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ContainsKey(TKey)
```csharp
public virtual bool ContainsKey(TKey key)
```
Returns `true` if the dictionary contains an entry for the given key.

**Parameters** \
`key` [TKey](../../) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Remove(TKey)
```csharp
public virtual bool Remove(TKey key)
```
Removes the entry for `key`; returns `true` if the key was present.

**Parameters** \
`key` [TKey](../../) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetValue(TKey, out TValue&)
```csharp
public virtual bool TryGetValue(TKey key, TValue& value)
```
Attempts to get the value for `key`; returns `true` and writes to `value` if found.

**Parameters** \
`key` [TKey](../../) \
`value` [TValue&](../../) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Add(TKey, TValue)
```csharp
public virtual void Add(TKey key, TValue value)
```
Adds a new key-value pair to the dictionary; throws if `key` already exists.

**Parameters** \
`key` [TKey](../../) \
`value` [TValue](../../) \

#### Clear()
```csharp
public virtual void Clear()
```
Removes all entries from the dictionary.

#### GetObjectData(SerializationInfo, StreamingContext)
```csharp
public virtual void GetObjectData(SerializationInfo info, StreamingContext context)
```
Populates `info` with the data needed to serialize this dictionary.

**Parameters** \
`info` [SerializationInfo](https://learn.microsoft.com/en-us/dotnet/api/System.Runtime.Serialization.SerializationInfo?view=net-7.0) \
`context` [StreamingContext](https://learn.microsoft.com/en-us/dotnet/api/System.Runtime.Serialization.StreamingContext?view=net-7.0) \

#### OnDeserialization(Object)
```csharp
public virtual void OnDeserialization(Object sender)
```
Called after the dictionary has been deserialized from a serialization stream.

**Parameters** \
`sender` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

#### TrimExcess()
```csharp
public void TrimExcess()
```
Resizes the internal arrays to eliminate any excess capacity.

#### TrimExcess(int)
```csharp
public void TrimExcess(int capacity)
```
Resizes the internal arrays to the given `capacity` if it is smaller than the current capacity.

**Parameters** \
`capacity` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡
# ComplexDictionary\<TKey, TValue\>

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public class ComplexDictionary<TKey, TValue> : Dictionary<TKey, TValue>, IDictionary<TKey, TValue>, ICollection<T>, IEnumerable<T>, IEnumerable, IDictionary, ICollection, IReadOnlyDictionary<TKey, TValue>, IReadOnlyCollection<T>, ISerializable, IDeserializationCallback
```

A plain, behaviorally-unmodified `Dictionary<TKey, TValue>` subclass whose only purpose is to be a distinct type that [ComplexDictionaryConverter\<T, V\>](../../Murder/Serialization/ComplexDictionaryConverter-2.html) can attach to.

**Intent:** `System.Text.Json` can only serialize dictionaries whose keys are `string` (or a small set of primitives it knows how to stringify). Murder needs dictionaries keyed by richer types — `Point` (pathfinding route maps in `RouteComponent`/`Astar`/`HAAStar`), `Type` (per-component overrides in `Murder.Prefabs.EntityModifier`), or value tuples (dialogue counters in `BlackboardTracker`) — which would throw at serialization time if stored as a regular `Dictionary<TKey, TValue>`. Using `ComplexDictionary<TKey, TValue>` instead makes the Murder serializer route it through `ComplexDictionaryConverter<T, V>`, which serializes each entry manually.

**Use-case:** Declare a field or property as `ComplexDictionary<TKey, TValue>` (instead of `Dictionary<TKey, TValue>`) anywhere the key type is not a `string`/primitive and the containing type needs to survive a round-trip through [MurderSerializerOptionsExtensions.Options](../../Murder/Serialization/MurderSerializerOptionsExtensions.html) — for example a serialized component field, a `GameAsset` property, or save data. Everywhere else in game logic it behaves exactly like `Dictionary<TKey, TValue>`, since it adds no members of its own.

**Implements:** _[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0), [IDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IDictionary-2?view=net-7.0), [ICollection\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.ICollection-1?view=net-7.0), [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0), [IEnumerable](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.IEnumerable?view=net-7.0), [IDictionary](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.IDictionary?view=net-7.0), [ICollection](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.ICollection?view=net-7.0), [IReadOnlyDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IReadOnlyDictionary-2?view=net-7.0), [IReadOnlyCollection\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IReadOnlyCollection-1?view=net-7.0), [ISerializable](https://learn.microsoft.com/en-us/dotnet/api/System.Runtime.Serialization.ISerializable?view=net-7.0), [IDeserializationCallback](https://learn.microsoft.com/en-us/dotnet/api/System.Runtime.Serialization.IDeserializationCallback?view=net-7.0)_

### ⭐ Constructors

```csharp
public ComplexDictionary<TKey, TValue>()
```

Creates an empty `ComplexDictionary` using the default equality comparer for `TKey`. Use this constructor (in place of a plain `Dictionary<TKey, TValue>`) whenever the containing type needs to be serialized with the Murder serializer options and `TKey` isn't a string/primitive.

```csharp
public ComplexDictionary<TKey, TValue>(IDictionary<TKey, TValue> dictionary)
```

Creates a `ComplexDictionary` pre-populated from an existing dictionary.

**Parameters** \
`dictionary` [IDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IDictionary-2?view=net-7.0) \

```csharp
public ComplexDictionary<TKey, TValue>(IEqualityComparer<TKey> comparer)
```

Creates an empty `ComplexDictionary` that uses `comparer` (instead of the default one) to determine key equality.

**Parameters** \
`comparer` [IEqualityComparer\<TKey\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEqualityComparer-1?view=net-7.0) \

### ⭐ Properties

#### Comparer

```csharp
public IEqualityComparer<TKey> Comparer { get; }
```

The equality comparer used to determine key equality in this dictionary.

**Returns** \
[IEqualityComparer\<TKey\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEqualityComparer-1?view=net-7.0) \

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

Gets or sets the value associated with the specified key. Throws `KeyNotFoundException` on get if the key isn't present.

**Returns** \
[TValue](../../) \

#### Keys

```csharp
public Dictionary<TKey, TValue>.KeyCollection Keys { get; }
```

The collection of all keys in this dictionary.

**Returns** \
[Dictionary\<TKey, TValue\>.KeyCollection](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2.KeyCollection?view=net-7.0) \

#### Values

```csharp
public Dictionary<TKey, TValue>.ValueCollection Values { get; }
```

The collection of all values in this dictionary.

**Returns** \
[Dictionary\<TKey, TValue\>.ValueCollection](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2.ValueCollection?view=net-7.0) \

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

#### Remove(TKey, TValue&)

```csharp
public bool Remove(TKey key, out TValue value)
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
public Dictionary<TKey, TValue>.Enumerator GetEnumerator()
```

Returns an enumerator that iterates through the key-value pairs in this dictionary.

**Returns** \
[Dictionary\<TKey, TValue\>.Enumerator](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2.Enumerator?view=net-7.0) \

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

#### TryGetValue(TKey, TValue&)

```csharp
public virtual bool TryGetValue(TKey key, out TValue value)
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

Populates `info` with the data needed to serialize this dictionary through the legacy `ISerializable`/binary-formatter path. Not used by the Murder JSON pipeline (that goes through `ComplexDictionaryConverter<T, V>` instead); present only because `Dictionary<TKey, TValue>` implements `ISerializable`.

**Parameters** \
`info` [SerializationInfo](https://learn.microsoft.com/en-us/dotnet/api/System.Runtime.Serialization.SerializationInfo?view=net-7.0) \
`context` [StreamingContext](https://learn.microsoft.com/en-us/dotnet/api/System.Runtime.Serialization.StreamingContext?view=net-7.0) \

#### OnDeserialization(Object)

```csharp
public virtual void OnDeserialization(Object sender)
```

Called after the dictionary has been deserialized through the legacy `ISerializable`/binary-formatter path; not invoked by `ComplexDictionaryConverter<T, V>`.

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

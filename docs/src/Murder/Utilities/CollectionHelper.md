# CollectionHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class CollectionHelper
```

Static helpers for building string-keyed dictionaries from collections with automatic duplicate-key disambiguation.

**Intent:** Provides safe dictionary construction from collections whose projected string keys may collide, automatically appending a numeric suffix to duplicates.

**Use-case:** Use `ToStringDictionary` when projecting a collection to a dictionary with potentially conflicting keys (e.g., asset names), avoiding silent overwrites.

### ⭐ Methods
#### ToStringDictionary(Dictionary`2&, IEnumerable<T>, Func<T, TResult>, Func<T, TResult>)
```csharp
public Dictionary<TKey, TValue> ToStringDictionary(Dictionary`2& existingDictionary, IEnumerable<T> collection, Func<T, TResult> toKey, Func<T, TResult> toValue)
```

Appends projected key-value pairs from `collection` into `existingDictionary`, disambiguating duplicate keys by appending a counter suffix.

**Parameters** \
`existingDictionary` [Dictionary\<TKey, TValue\>&](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
`collection` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
`toKey` [Func\<T, TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \
`toValue` [Func\<T, TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

#### ToStringDictionary(IEnumerable<T>, Func<T, TResult>, Func<T, TResult>)
```csharp
public Dictionary<TKey, TValue> ToStringDictionary(IEnumerable<T> collection, Func<T, TResult> toKey, Func<T, TResult> toValue)
```

Creates a new string-keyed dictionary by projecting `collection`, with automatic counter suffixes added to any duplicate keys.

**Parameters** \
`collection` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
`toKey` [Func\<T, TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \
`toValue` [Func\<T, TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \



⚡
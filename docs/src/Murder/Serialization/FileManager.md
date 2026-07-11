# FileManager

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public class FileManager
```

FileHelper which will do OS operations. This is system-agnostic.

**Intent:** Provides system-agnostic file I/O methods for reading, writing, and managing game asset and save files.

**Use-case:** Access via `Game.Data.FileManager` to serialize assets to JSON, deserialize from disk, pack/unpack compressed content archives, and manage directories.

### ⭐ Constructors
```csharp
public FileManager()
```
Creates a new `FileManager` instance.

### ⭐ Methods
#### FileExistsWithCaseInsensitive(String&)
```csharp
protected virtual bool FileExistsWithCaseInsensitive(String& path)
```
Returns `true` if a file exists at `path`, performing a case-insensitive match on case-sensitive file systems.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DeleteDirectoryIfExists(String&)
```csharp
public bool DeleteDirectoryIfExists(String& path)
```
Deletes the directory at `path` and all its contents if it exists; returns `true` if deleted.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DeleteFileIfExists(String&)
```csharp
public bool DeleteFileIfExists(String& path)
```
Deletes the file at `path` if it exists; returns `true` if the file was deleted.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Exists(String&)
```csharp
public bool Exists(String& path)
```
Returns `true` if a file or directory exists at `path`.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetOrCreateDirectory(String&)
```csharp
public DirectoryInfo GetOrCreateDirectory(String& path)
```
Returns the `DirectoryInfo` for `path`, creating the directory and all parents if they do not exist.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[DirectoryInfo](https://learn.microsoft.com/en-us/dotnet/api/System.IO.DirectoryInfo?view=net-7.0) \

#### ListAllDirectories(string)
```csharp
public IEnumerable<T> ListAllDirectories(string path)
```
Enumerates all subdirectories within `path`.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### SaveSerialized(T, string)
```csharp
public string SaveSerialized(T value, string path)
```
Serializes `value` to JSON and writes it to `path`; returns the path on success.

**Parameters** \
`value` [T](../../) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SerializeToJson(T)
```csharp
public string SerializeToJson(T value)
```
Serializes `value` to a JSON string using the Murder serializer options.

**Parameters** \
`value` [T](../../) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### DeserializeAsset(string)
```csharp
public T DeserializeAsset(string path)
```
Deserializes a `GameAsset` subclass from the file at `path`.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T](../../) \

#### DeserializeFromJson(Stream)
```csharp
public T DeserializeFromJson(Stream stream)
```
Deserializes an object of type `T` from a JSON `Stream`.

**Parameters** \
`stream` [Stream](https://learn.microsoft.com/en-us/dotnet/api/System.IO.Stream?view=net-7.0) \

**Returns** \
[T](../../) \

#### DeserializeFromJson(string)
```csharp
public T DeserializeFromJson(string json)
```
Deserializes an object of type `T` from a raw JSON string.

**Parameters** \
`json` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T](../../) \

#### DeserializeGeneric(string, bool)
```csharp
public T DeserializeGeneric(string path, bool warnOnErrors)
```
Deserializes an object of type `T` from the file at `path`; logs a warning on parse errors when `warnOnErrors` is `true`.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`warnOnErrors` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[T](../../) \

#### UnpackContent(string)
```csharp
public T UnpackContent(string path)
```

Unpack content from a zip format. This reduces the overhead on IO time.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T](../../) \

#### PackContentAsync(string, string)
```csharp
public Task PackContentAsync(string json, string path)
```

Pack json content into a zip format that will be compressed and reduce IO time.

**Parameters** \
`json` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### SaveTextAsync(string, string)
```csharp
public Task SaveTextAsync(string fullpath, string content)
```
Writes `content` as UTF-8 text to `fullpath` asynchronously.

**Parameters** \
`fullpath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`content` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### DeserializeAssetAsync(string)
```csharp
public Task<TResult> DeserializeAssetAsync(string path)
```

Deserialize and asset asynchronously. Assumes that <paramref name="path" /> is valid.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Task\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task-1?view=net-7.0) \

#### SaveSerializedAsync(T, string)
```csharp
public ValueTask<TResult> SaveSerializedAsync(T value, string path)
```

**Parameters** \
`value` [T](../../) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ValueTask\<TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask-1?view=net-7.0) \

#### CreateDirectoryPathIfNotExists(string)
```csharp
public void CreateDirectoryPathIfNotExists(string filePath)
```

This will create a directory on the root of this <paramref name="filePath" />,
            if the directory is not available.

**Parameters** \
`filePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### DeleteContent(String&, bool)
```csharp
public void DeleteContent(String& fullpath, bool deleteRootFiles)
```

**Parameters** \
`fullpath` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`deleteRootFiles` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PackContent(T, string)
```csharp
public void PackContent(T data, string path)
```

**Parameters** \
`data` [T](../../) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SaveText(String&, String&)
```csharp
public void SaveText(String& fullpath, String& content)
```

**Parameters** \
`fullpath` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`content` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SerializeToJson(Stream, T)
```csharp
public void SerializeToJson(Stream stream, T value)
```

**Parameters** \
`stream` [Stream](https://learn.microsoft.com/en-us/dotnet/api/System.IO.Stream?view=net-7.0) \
`value` [T](../../) \



⚡
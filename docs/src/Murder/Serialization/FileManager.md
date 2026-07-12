# FileManager

**Namespace:** Murder.Serialization \
**Assembly:** Murder.dll

```csharp
public partial class FileManager
```

The engine's system-agnostic entry point for reading, writing, and managing files: JSON (de)serialization of assets and arbitrary objects, compressed "packed content" archives, and directory/file management.

**Intent:** Give the rest of the engine a single, overridable place to perform disk I/O, instead of scattering `File`/`Directory` calls everywhere. Being a regular (non-static, instance) class also lets it be subclassed — the editor uses `EditorFileManager : FileManager` to override case-sensitivity behavior for the editor's file browsing.

**Use-case:** Access the shared instance via `Game.Data.FileManager` (or the editor's `Architect.EditorData.FileManager`) to serialize assets/save data to JSON, deserialize them back, pack/unpack compressed content archives, and create/delete directories and files. The static `SerializeToJson`/`DeserializeFromJson` overloads can also be called directly (e.g. `Murder.Serialization.FileManager.SerializeToJson(value)`) when you just need JSON text or stream I/O without touching the file system.

### ⭐ Constructors

```csharp
public FileManager()
```

Implicit public constructor; `FileManager` has no state of its own, so a new instance is simply a fresh binding to the static serialization helpers and overridable file-existence behavior.

### ⭐ Methods

#### PackContent\<T\>(T, string)

```csharp
public void PackContent<T>(T data, string path)
```

Serializes `data` to JSON and writes it, GZip-compressed, to `path`. Used for content that would otherwise be a large, human-editable JSON file (e.g. packed save data or exported content archives) where disk size and load time matter more than readability. Pair with `UnpackContent<T>(string)` to read it back.

**Parameters** \
`data` [T](../../) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PackContentAsync(string, string)

```csharp
public async Task PackContentAsync(string json, string path)
```

Writes an already-serialized `json` string, GZip-compressed, to `path` without blocking the calling thread. Use this instead of `PackContent<T>(T, string)` when you already have the JSON text (e.g. produced ahead of time) and want to avoid blocking I/O.

**Parameters** \
`json` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### UnpackContent\<T\>(string)

```csharp
public T? UnpackContent<T>(string path)
```

Reads and GZip-decompresses the file at `path`, then deserializes it into a `T`. The counterpart to `PackContent<T>(T, string)`.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T](../../) \

#### SaveText(String&, String&)

```csharp
public void SaveText(in string fullpath, in string content)
```

Writes `content` as UTF-8 text to `fullpath`, creating the containing directory first if it does not already exist. `fullpath` must be an absolute, rooted path (see `FileHelper.GetPath(string[])`). This is the low-level primitive behind `SaveSerialized<T>(T, string)`; call it directly when you already have a raw string to persist and don't need JSON serialization.

**Parameters** \
`fullpath` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`content` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SaveTextAsync(string, string)

```csharp
public async Task SaveTextAsync(string fullpath, string content)
```

Asynchronous counterpart of `SaveText`: writes `content` as UTF-8 text to `fullpath` without blocking the calling thread, creating the containing directory first if needed. Prefer this over `SaveText` on hot paths (e.g. autosave) where blocking I/O could cause a frame hitch.

**Parameters** \
`fullpath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`content` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### SerializeToJson\<T\>(T)

```csharp
public static string SerializeToJson<T>(T value)
```

Serializes `value` to an indented JSON string using `Game.Data.SerializationOptions` (every Murder component/asset converter plus the source-generated type metadata). The core primitive underneath `SaveSerialized<T>(T, string)`; call it directly when you need the JSON text itself rather than writing it straight to a file.

**Parameters** \
`value` [T](../../) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### DeserializeFromJson\<T\>(string)

```csharp
public static T? DeserializeFromJson<T>(string json)
```

Deserializes `json` into a `T` using `Game.Data.SerializationOptions`. Unlike `DeserializeGeneric<T>(string, bool)`, this takes the raw JSON text directly (not a file path) and does not catch parse errors — use it when you already have JSON in memory (e.g. from the clipboard or network) and want exceptions to propagate.

**Parameters** \
`json` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T](../../) \

#### SerializeToJson\<T\>(Stream, T)

```csharp
public static void SerializeToJson<T>(Stream stream, T value)
```

Serializes `value` as JSON directly to `stream` using `Game.Data.SerializationOptions`, avoiding the extra intermediate string allocation `SerializeToJson<T>(T)` would incur. Used by `PackContent<T>(T, string)` to stream straight into a `GZipStream`.

**Parameters** \
`stream` [Stream](https://learn.microsoft.com/en-us/dotnet/api/System.IO.Stream?view=net-7.0) \
`value` [T](../../) \

#### DeserializeFromJson\<T\>(Stream)

```csharp
public static T? DeserializeFromJson<T>(Stream stream)
```

Deserializes a `T` directly from `stream` using `Game.Data.SerializationOptions`, avoiding the extra intermediate string allocation `DeserializeFromJson<T>(string)` would incur. Used by `UnpackContent<T>(string)` to read straight out of a decompression stream.

**Parameters** \
`stream` [Stream](https://learn.microsoft.com/en-us/dotnet/api/System.IO.Stream?view=net-7.0) \

**Returns** \
[T](../../) \

#### SaveSerialized\<T\>(T, string)

```csharp
public string SaveSerialized<T>(T value, string path)
```

Serializes `value` to indented JSON and writes it to `path`, returning the JSON text that was written (in case the caller also wants to log or hash it). This is the standard way to persist any serializable Murder object — assets, save data, editor settings — to disk.

**Parameters** \
`value` [T](../../) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SaveSerializedAsync\<T\>(T, string)

```csharp
public async ValueTask<string> SaveSerializedAsync<T>(T value, string path)
```

Asynchronous counterpart of `SaveSerialized<T>(T, string)`: serializes `value` to JSON and writes it to `path` without blocking the calling thread. Prefer this for autosave/background-save flows so serialization and disk I/O don't stall the game loop.

**Parameters** \
`value` [T](../../) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ValueTask\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.ValueTask-1?view=net-7.0) \

#### DeserializeGeneric\<T\>(string, bool)

```csharp
public T? DeserializeGeneric<T>(string path, bool warnOnErrors = true)
```

Deserializes the JSON file at `path` into a `T`. Unlike `DeserializeAsset<T>(string)`, `T` is not constrained to `GameAsset`, so this is used for any plain serializable object (editor settings, save data, etc.) rather than game assets specifically. Returns `default` without throwing when the file is missing or fails to parse; pass `warnOnErrors: false` to suppress the "file not found" log for callers that probe for optional files.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`warnOnErrors` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[T](../../) \

#### DeserializeAssetAsync\<T\>(string)

```csharp
public async Task<T?> DeserializeAssetAsync<T>(string path) where T : GameAsset
```

Reads and deserializes a [GameAsset](../../Murder/Assets/GameAsset.html)-derived asset from `path` without blocking the calling thread, calling `AfterDeserialized()` on it and assigning a fresh `Guid` if the asset was saved without one. Assumes `path` is valid (does not check existence first); returns `null` if the JSON fails to parse.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Task\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task-1?view=net-7.0) \

#### DeserializeAsset\<T\>(string)

```csharp
public T? DeserializeAsset<T>(string path) where T : GameAsset
```

Synchronous counterpart of `DeserializeAssetAsync<T>(string)`: reads and deserializes a [GameAsset](../../Murder/Assets/GameAsset.html)-derived asset from `path`, calling `AfterDeserialized()` and assigning a fresh `Guid` if needed. Returns `null` instead of throwing if the file is missing or the JSON fails to parse, so callers can treat a bad/missing asset file as "not loaded" rather than a fatal error.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T](../../) \

#### ListAllDirectories(string)

```csharp
public static IEnumerable<string> ListAllDirectories(string path)
```

Returns the full paths of every immediate subdirectory of `path`, or an empty sequence if `path` does not exist (rather than throwing). Used by editor/asset-scanning code that needs to enumerate content folders defensively.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[IEnumerable\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### GetOrCreateDirectory(String&)

```csharp
public static DirectoryInfo GetOrCreateDirectory(in string path)
```

Returns the `DirectoryInfo` for `path`, creating it and any missing parent directories first if it does not already exist. The general-purpose "make sure this directory is there" helper used throughout this class's file-writing paths.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[DirectoryInfo](https://learn.microsoft.com/en-us/dotnet/api/System.IO.DirectoryInfo?view=net-7.0) \

#### DeleteDirectoryIfExists(String&)

```csharp
public static bool DeleteDirectoryIfExists(in string path)
```

Recursively deletes the directory at `path` (and everything inside it) if it exists. Returns `false` both when the directory did not exist and when deletion failed (e.g. a file inside is locked); a warning is logged in the latter case.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FileExistsWithCaseInsensitive(String&)

```csharp
protected virtual bool FileExistsWithCaseInsensitive(in string path)
```

Returns `true` if a file exists at `path`. On case-sensitive file systems this still performs an exact match by default (it simply wraps `File.Exists`); it is declared `virtual` and `protected` specifically so that `EditorFileManager` can override it with a genuinely case-insensitive search, since editor tooling routinely receives paths whose casing doesn't match the file on disk.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DeleteFileIfExists(String&)

```csharp
public bool DeleteFileIfExists(in string path)
```

Deletes the file at `path` if it exists (via `FileExistsWithCaseInsensitive`), returning `true` only if a file was actually deleted.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Exists(String&)

```csharp
public bool Exists(in string path)
```

Returns `true` if a file exists at `path`, using the same (possibly overridden) case-insensitive check as the rest of this class. Despite the generic name, this only checks for files — use `Directory.Exists(string)` directly to test for a directory.

**Parameters** \
`path` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CreateDirectoryPathIfNotExists(string)

```csharp
public static void CreateDirectoryPathIfNotExists(string filePath)
```

Creates the directory that would contain `filePath` (i.e. `Path.GetDirectoryName(filePath)`), if it does not already exist. Use this before writing to a file whose parent folder may not have been created yet.

**Parameters** \
`filePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### DeleteContent(String&, bool)

```csharp
public static void DeleteContent(in string fullpath, bool deleteRootFiles)
```

Deletes every subdirectory inside `fullpath` (recursively), and — when `deleteRootFiles` is `true` — every file directly inside `fullpath` as well, without deleting `fullpath` itself. Used to clear out a previous packed/exported content folder before writing a fresh one.

**Parameters** \
`fullpath` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — complete rooted path. \
`deleteRootFiles` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — whether the files directly inside `fullpath` should also be deleted. \

⚡

# IPreview

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public abstract IPreview
```

This is an interface implemented by assets which has a preview in the editor.

**Intent:** Mark an asset as previewable so the editor can call `GetPreviewId` to render a thumbnail without knowing the concrete type.

**Use-case:** Implement `IPreview` on a `GameAsset` subclass (e.g. `SpriteAsset`) to enable editor thumbnail previews. The editor detects the interface and calls `GetPreviewId` to obtain the atlas/sprite pair needed to render the preview image.

### ⭐ Methods
#### GetPreviewId()
```csharp
public abstract ValueTuple<T1, T2> GetPreviewId()
```

Returns the preview id to show this image.

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \



⚡
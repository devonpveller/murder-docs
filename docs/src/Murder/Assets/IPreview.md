# IPreview

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public abstract IPreview
```

Implemented by assets that can render a thumbnail preview in the editor's asset browser (e.g. `SpriteAsset`).

**Intent:** Let editor helper code check for this interface and draw a thumbnail without knowing the concrete asset type.

**Use-case:** Implement `IPreview` on a `GameAsset` subclass to enable editor thumbnail previews. The editor's `EditorAssetsHelpers.DrawPreview` helper detects the interface and calls `GetPreviewId` to obtain the atlas/frame pair needed to render the preview image.

### ⭐ Methods

#### GetPreviewId()

```csharp
public abstract ValueTuple<T1, T2> GetPreviewId()
```

Returns the `(atlas id, frame/image id)` pair identifying which atlas image should be drawn as this asset's thumbnail. The editor looks up the actual texture region using these two ids.

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

⚡

# wbDDSResourceToBitmap

## Syntax

```pascal
function wbDDSResourceToBitmap(aResourceName: string; aBitmap: TBitmap): Boolean;
```

## Description

Converts a DDS texture stored in a BSA or BA2 archive directly to a Windows bitmap. This is a convenience wrapper that opens the resource data and calls wbDDSDataToBitmap internally.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aResourceName | string | The path to the DDS file within archives |
| aBitmap | TBitmap | The target bitmap object to receive the decoded image |

## Returns

Returns True if the DDS resource was successfully loaded and converted to a bitmap, False otherwise.

## Example

```pascal
var
  bitmap: TBitmap;
begin
  bitmap := TBitmap.Create;
  try
    if wbDDSResourceToBitmap('textures\landscape\grass01.dds', bitmap) then begin
      AddMessage('Texture loaded: ' + IntToStr(bitmap.Width) + 'x' + IntToStr(bitmap.Height));
      bitmap.SaveToFile(TempPath + 'grass_preview.bmp');
    end;
  finally
    bitmap.Free;
  end;
end;
```

## See Also

- [wbDDSDataToBitmap](IwbResource_wbDDSDataToBitmap.md)
- [wbDDSStreamToBitmap](IwbResource_wbDDSStreamToBitmap.md)
- [ResourceOpenData](IwbContainer_ResourceOpenData.md)

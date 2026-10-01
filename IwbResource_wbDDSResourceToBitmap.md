# wbDDSResourceToBitmap

## Syntax

```pascal
function wbDDSResourceToBitmap(AResourceName: string; ABitmap: TBitmap): Boolean;
```

## Description

Opens a DDS with an empty container name, the same last-loaded match as [ResourceOpenData](IwbResource_ResourceOpenData.md), and passes the bytes to [wbDDSDataToBitmap](IwbResource_wbDDSDataToBitmap.md). A missing file yields empty bytes and this function returns False.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AResourceName | string | The path to the DDS file within archives |
| ABitmap | TBitmap | The target bitmap object to receive the decoded image |

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
- [ResourceOpenData](IwbResource_ResourceOpenData.md)

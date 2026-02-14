# wbDDSDataToBitmap

## Syntax

```pascal
function wbDDSDataToBitmap(AData: TBytes; ABitmap: TBitmap): Boolean;
```

## Description

Converts DDS (DirectDraw Surface) texture data to a standard Windows bitmap. This function decodes the compressed DDS format and renders it to a TBitmap object for display or processing.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AData | TBytes | The raw binary data of the DDS file |
| ABitmap | TBitmap | The target bitmap object to receive the decoded image |

## Returns

Returns True if the DDS data was successfully decoded and converted to a bitmap, False otherwise.

## Example

```pascal
var
  ddsData: TBytes;
  bitmap: TBitmap;
begin
  bitmap := TBitmap.Create;
  try
    ddsData := ResourceOpenData('', 'textures\armor\iron\ironarmor_d.dds');

    if wbDDSDataToBitmap(ddsData, bitmap) then begin
      AddMessage('DDS decoded: ' + IntToStr(bitmap.Width) + 'x' + IntToStr(bitmap.Height));
      bitmap.SaveToFile(TempPath + 'preview.bmp');
    end;
  finally
    bitmap.Free;
  end;
end;
```

## See Also

- [wbDDSResourceToBitmap](IwbResource_wbDDSResourceToBitmap.md)
- [wbDDSStreamToBitmap](IwbResource_wbDDSStreamToBitmap.md)

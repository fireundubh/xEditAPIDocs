# wbDDSStreamToBitmap

## Syntax

```pascal
function wbDDSStreamToBitmap(aStream: TStream; aBitmap: TBitmap): Boolean;
```

## Description

Converts DDS texture data from a stream to a Windows bitmap. This function reads the DDS format from any TStream descendant and decodes it to a TBitmap object.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aStream | TStream | The stream containing the DDS data |
| aBitmap | TBitmap | The target bitmap object to receive the decoded image |

## Returns

Returns True if the DDS stream was successfully decoded and converted to a bitmap, False otherwise.

## Example

```pascal
var
  fileStream: TFileStream;
  bitmap: TBitmap;
begin
  bitmap := TBitmap.Create;
  fileStream := TFileStream.Create(DataPath + 'Textures\custom.dds', fmOpenRead);
  try
    if wbDDSStreamToBitmap(fileStream, bitmap) then
      AddMessage('Stream decoded to bitmap successfully');
  finally
    fileStream.Free;
    bitmap.Free;
  end;
end;
```

## See Also

- [wbDDSDataToBitmap](IwbResource_wbDDSDataToBitmap.md)
- [wbDDSResourceToBitmap](IwbResource_wbDDSResourceToBitmap.md)

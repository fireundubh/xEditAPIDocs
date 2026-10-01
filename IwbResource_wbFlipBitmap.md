# wbFlipBitmap

## Syntax

```pascal
procedure wbFlipBitmap(ABitmap: TBitmap; ADirection: Integer);
```

## Description

Flips a bitmap in place. `0` flips both ways, `1` flips left to right, and `2` flips top to bottom. A nil bitmap is ignored. Use one of those three values.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABitmap | TBitmap | The bitmap to flip |
| ADirection | Integer | 0 flips both ways. 1 flips left to right. 2 flips top to bottom |

## Returns

This function does not return a value.

## Example

```pascal
var
  bitmap: TBitmap;
begin
  bitmap := TBitmap.Create;
  try
    if wbDDSResourceToBitmap('textures\effects\gradient.dds', bitmap) then begin
      // 1 flips left to right
      wbFlipBitmap(bitmap, 1);
      bitmap.SaveToFile(wbTempPath + 'flipped.bmp');
    end;
  finally
    bitmap.Free;
  end;
end;
```

## See Also

- [wbAlphaBlend](IwbResource_wbAlphaBlend.md)

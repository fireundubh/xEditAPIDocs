# wbFlipBitmap

## Syntax

```pascal
procedure wbFlipBitmap(aBitmap: TBitmap; aDirection: Integer);
```

## Description

Flips a bitmap image horizontally or vertically. This function modifies the bitmap in place, creating a mirror image along the specified axis.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aBitmap | TBitmap | The bitmap to flip |
| aDirection | Integer | Direction to flip: 0=horizontal, 1=vertical |

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
      // Flip horizontally
      wbFlipBitmap(bitmap, 0);
      bitmap.SaveToFile(TempPath + 'flipped.bmp');
    end;
  finally
    bitmap.Free;
  end;
end;
```

## See Also

- [wbAlphaBlend](IwbResource_wbAlphaBlend.md)

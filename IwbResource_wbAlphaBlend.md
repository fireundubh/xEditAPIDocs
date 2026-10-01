# wbAlphaBlend

## Syntax

```pascal
function wbAlphaBlend(DestDC: HDC; X, Y, Width, Height: Integer; SrcDC: HDC; SrcX, SrcY, SrcWidth, SrcHeight: Integer; Alpha: Byte): Boolean;
```

## Description

Blends a rectangle from one device context onto another. `Alpha` is the constant source alpha, from 0 (fully transparent) to 255 (opaque). A value of 255 also uses per-pixel alpha. Any lower value uses constant alpha only.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| DestDC | HDC | Handle to the destination device context |
| X | Integer | X-coordinate of the upper-left corner of the destination rectangle |
| Y | Integer | Y-coordinate of the upper-left corner of the destination rectangle |
| Width | Integer | Width of the destination rectangle |
| Height | Integer | Height of the destination rectangle |
| SrcDC | HDC | Handle to the source device context |
| SrcX | Integer | X-coordinate of the upper-left corner of the source rectangle |
| SrcY | Integer | Y-coordinate of the upper-left corner of the source rectangle |
| SrcWidth | Integer | Width of the source rectangle |
| SrcHeight | Integer | Height of the source rectangle |
| Alpha | Byte | Alpha transparency value (0=transparent, 255=opaque) |

## Returns

Returns True if the operation succeeded, False otherwise.

## Example

```pascal
var
  destBitmap, srcBitmap: TBitmap;
begin
  destBitmap := TBitmap.Create;
  srcBitmap := TBitmap.Create;
  try
    // Load bitmaps
    srcBitmap.LoadFromFile(DataPath + 'Textures\overlay.bmp');

    // Blend with 50% opacity
    wbAlphaBlend(destBitmap.Canvas.Handle, 0, 0, destBitmap.Width, destBitmap.Height,
                 srcBitmap.Canvas.Handle, 0, 0, srcBitmap.Width, srcBitmap.Height, 128);
  finally
    destBitmap.Free;
    srcBitmap.Free;
  end;
end;
```

## See Also

- [wbFlipBitmap](IwbResource_wbFlipBitmap.md)

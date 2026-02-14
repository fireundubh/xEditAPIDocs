# wbAlphaBlend

## Syntax

```pascal
function wbAlphaBlend(DestDC: HDC; X, Y, Width, Height: Integer; SrcDC: HDC; SrcX, SrcY, SrcWidth, SrcHeight: Integer; Alpha: Byte): Boolean;
```

## Description

Performs alpha blending between two device contexts, copying a rectangular region from the source DC to the destination DC with specified transparency. This is a wrapper around the Windows AlphaBlend API function.

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

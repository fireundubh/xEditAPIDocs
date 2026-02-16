# Graphics & Drawing Reference

Graphics classes for drawing, images, fonts, colors, and visual elements in xEdit scripts.

**Units:** Graphics

[← Back to Standard Library Overview](stdlib_home.md)

## Table of Contents

- [Color Functions](#color-functions)
- [TCanvas - Drawing Surface](#tcanvas---drawing-surface)
- [TBitmap - Bitmap Images](#tbitmap---bitmap-images)
- [TFont - Text Fonts](#tfont---text-fonts)
- [TPen - Drawing Pen](#tpen---drawing-pen)
- [TBrush - Fill Brush](#tbrush---fill-brush)
- [TPicture - Image Container](#tpicture---image-container)
- [xEdit Visualization Examples](#xedit-visualization-examples)

## Color Functions

Color manipulation functions.

| Function | Signature | Description |
|----------|-----------|-------------|
| `RGB` | `RGB(Red, Green, Blue: Byte): TColor` | Create color from RGB values (0-255) |
| `ColorToRGB` | `ColorToRGB(Color: TColor): Longint` | Convert to RGB value |
| `GetRValue` | `GetRValue(RGB: DWORD): Byte` | Extract red component |
| `GetGValue` | `GetGValue(RGB: DWORD): Byte` | Extract green component |
| `GetBValue` | `GetBValue(RGB: DWORD): Byte` | Extract blue component |

### Standard Color Constants

```pascal
clBlack      = $000000;
clMaroon     = $000080;
clGreen      = $008000;
clOlive      = $008080;
clNavy       = $800000;
clPurple     = $800080;
clTeal       = $808000;
clGray       = $808080;
clSilver     = $C0C0C0;
clRed        = $0000FF;
clLime       = $00FF00;
clYellow     = $00FFFF;
clBlue       = $FF0000;
clFuchsia    = $FF00FF;
clAqua       = $FFFF00;
clWhite      = $FFFFFF;
```

### System Color Constants

```pascal
clScrollBar        = COLOR_SCROLLBAR or $80000000;
clBackground       = COLOR_BACKGROUND or $80000000;
clActiveCaption    = COLOR_ACTIVECAPTION or $80000000;
clInactiveCaption  = COLOR_INACTIVECAPTION or $80000000;
clMenu             = COLOR_MENU or $80000000;
clWindow           = COLOR_WINDOW or $80000000;
clWindowFrame      = COLOR_WINDOWFRAME or $80000000;
clMenuText         = COLOR_MENUTEXT or $80000000;
clWindowText       = COLOR_WINDOWTEXT or $80000000;
clCaptionText      = COLOR_CAPTIONTEXT or $80000000;
clActiveBorder     = COLOR_ACTIVEBORDER or $80000000;
clInactiveBorder   = COLOR_INACTIVEBORDER or $80000000;
clAppWorkSpace     = COLOR_APPWORKSPACE or $80000000;
clHighlight        = COLOR_HIGHLIGHT or $80000000;
clHighlightText    = COLOR_HIGHLIGHTTEXT or $80000000;
clBtnFace          = COLOR_BTNFACE or $80000000;
clBtnShadow        = COLOR_BTNSHADOW or $80000000;
clGrayText         = COLOR_GRAYTEXT or $80000000;
clBtnText          = COLOR_BTNTEXT or $80000000;
clBtnHighlight     = COLOR_BTNHIGHLIGHT or $80000000;
cl3DDkShadow       = COLOR_3DDKSHADOW or $80000000;
cl3DLight          = COLOR_3DLIGHT or $80000000;
clInfoText         = COLOR_INFOTEXT or $80000000;
clInfoBk           = COLOR_INFOBK or $80000000;
```

### Color Example

```pascal
// Create custom colors
var
  color: TColor;
  r, g, b: Byte;
begin
  // Create from RGB
  color := RGB(255, 128, 64);  // Orange

  // Extract components
  r := GetRValue(ColorToRGB(color));  // 255
  g := GetGValue(ColorToRGB(color));  // 128
  b := GetBValue(ColorToRGB(color));  // 64

  AddMessage(Format('RGB: %d, %d, %d', [r, g, b]));
end;
```

## TCanvas - Drawing Surface

TCanvas provides a drawing surface for forms, bitmaps, and other visual components.

Access via: `Form.Canvas`, `Bitmap.Canvas`, `PaintBox.Canvas`, etc.

### Drawing Methods

#### Lines and Shapes

| Method | Signature | Description |
|--------|-----------|-------------|
| `MoveTo` | `MoveTo(X, Y: Integer)` | Move pen to position |
| `LineTo` | `LineTo(X, Y: Integer)` | Draw line from current position |
| `Line` | `Line(X1, Y1, X2, Y2: Integer)` | Draw line between points |
| `Polyline` | `Polyline(Points: array of TPoint)` | Draw connected lines |
| `Rectangle` | `Rectangle(X1, Y1, X2, Y2: Integer)` | Draw rectangle |
| `RoundRect` | `RoundRect(X1, Y1, X2, Y2, X3, Y3: Integer)` | Draw rounded rectangle |
| `Ellipse` | `Ellipse(X1, Y1, X2, Y2: Integer)` | Draw ellipse/circle |
| `Arc` | `Arc(X1, Y1, X2, Y2, X3, Y3, X4, Y4: Integer)` | Draw arc |
| `Chord` | `Chord(X1, Y1, X2, Y2, X3, Y3, X4, Y4: Integer)` | Draw chord |
| `Pie` | `Pie(X1, Y1, X2, Y2, X3, Y3, X4, Y4: Integer)` | Draw pie slice |
| `Polygon` | `Polygon(Points: array of TPoint)` | Draw filled polygon |

#### Fill and Flood

| Method | Signature | Description |
|--------|-----------|-------------|
| `FillRect` | `FillRect(Rect: TRect)` | Fill rectangle |
| `FloodFill` | `FloodFill(X, Y: Integer, Color: TColor, FillStyle: TFillStyle)` | Flood fill area |
| `FrameRect` | `FrameRect(Rect: TRect)` | Draw rectangle frame |

#### Text

| Method | Signature | Description |
|--------|-----------|-------------|
| `TextOut` | `TextOut(X, Y: Integer, Text: string)` | Draw text at position |
| `TextRect` | `TextRect(Rect: TRect, X, Y: Integer, Text: string)` | Draw text clipped to rectangle |
| `TextWidth` | `TextWidth(Text: string): Integer` | Get text width |
| `TextHeight` | `TextHeight(Text: string): Integer` | Get text height |
| `TextExtent` | `TextExtent(Text: string): TSize` | Get text size |

#### Images

| Method | Signature | Description |
|--------|-----------|-------------|
| `Draw` | `Draw(X, Y: Integer, Graphic: TGraphic)` | Draw graphic at position |
| `StretchDraw` | `StretchDraw(Rect: TRect, Graphic: TGraphic)` | Draw graphic stretched |
| `CopyRect` | `CopyRect(Dest: TRect, Canvas: TCanvas, Source: TRect)` | Copy from another canvas |

#### Pixels

| Method | Signature | Description |
|--------|-----------|-------------|
| `Pixels[X, Y]` | `property Pixels[X, Y: Integer]: TColor` | Get/set pixel color |

### Canvas Properties

| Property | Type | Description |
|----------|------|-------------|
| `Pen` | TPen | Drawing pen |
| `Brush` | TBrush | Fill brush |
| `Font` | TFont | Text font |
| `PenPos` | TPoint | Current pen position |
| `ClipRect` | TRect | Clipping rectangle |

### TRect and TPoint

```pascal
// TRect - Rectangle
TRect = record
  Left, Top, Right, Bottom: Integer;
end;

// TPoint - Point
TPoint = record
  X, Y: Integer;
end;

// Helper functions
function Rect(Left, Top, Right, Bottom: Integer): TRect;
function Point(X, Y: Integer): TPoint;
```

### Canvas Drawing Example

```pascal
// Draw on form canvas
procedure TForm1.FormPaint(Sender: TObject);
var
  canvas: TCanvas;
begin
  canvas := TForm1(Sender).Canvas;

  // Set pen and brush
  canvas.Pen.Color := clBlack;
  canvas.Pen.Width := 2;
  canvas.Brush.Color := clYellow;

  // Draw shapes
  canvas.Rectangle(10, 10, 100, 100);
  canvas.Ellipse(120, 10, 210, 100);

  // Draw line
  canvas.MoveTo(10, 120);
  canvas.LineTo(210, 120);

  // Draw text
  canvas.Font.Size := 14;
  canvas.Font.Style := [fsBold];
  canvas.TextOut(10, 140, 'Hello World');
end;
```

## TBitmap - Bitmap Images

TBitmap manages bitmap images in memory.

**Constructor:**
```pascal
bmp := TBitmap.Create;
```

### Properties

| Property | Type | Description |
|----------|------|-------------|
| `Width` | Integer | Bitmap width in pixels |
| `Height` | Integer | Bitmap height in pixels |
| `Canvas` | TCanvas | Drawing surface |
| `PixelFormat` | TPixelFormat | Pixel format (pf1bit, pf4bit, pf8bit, pf16bit, pf24bit, pf32bit) |
| `Transparent` | Boolean | Enable transparency |
| `TransparentColor` | TColor | Transparent color |
| `TransparentMode` | TTransparentMode | Transparency mode |

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `LoadFromFile` | `LoadFromFile(FileName: string)` | Load from file |
| `SaveToFile` | `SaveToFile(FileName: string)` | Save to file |
| `LoadFromStream` | `LoadFromStream(Stream: TStream)` | Load from stream |
| `SaveToStream` | `SaveToStream(Stream: TStream)` | Save to stream |
| `Assign` | `Assign(Source: TPersistent)` | Copy from another bitmap |
| `SetSize` | `SetSize(AWidth, AHeight: Integer)` | Resize bitmap |

### Bitmap Example

```pascal
// Create and manipulate bitmap
var
  bmp: TBitmap;
  x, y: Integer;
begin
  bmp := TBitmap.Create;
  try
    // Create blank bitmap
    bmp.Width := 200;
    bmp.Height := 200;
    bmp.PixelFormat := pf24bit;

    // Fill with gradient
    for y := 0 to bmp.Height - 1 do
      for x := 0 to bmp.Width - 1 do
        bmp.Canvas.Pixels[x, y] := RGB(x, y, 128);

    // Draw on bitmap
    bmp.Canvas.Pen.Color := clRed;
    bmp.Canvas.Pen.Width := 3;
    bmp.Canvas.Ellipse(50, 50, 150, 150);

    // Save to file
    bmp.SaveToFile(wbDataPath + 'output.bmp');

    AddMessage('Bitmap created and saved');
  finally
    bmp.Free;
  end;
end;
```

### Load and Display Bitmap

```pascal
// Load bitmap and show in TImage
var
  bmp: TBitmap;
  img: TImage;
  form: TForm;
begin
  form := TForm.Create(nil);
  try
    form.Width := 400;
    form.Height := 400;
    form.Caption := 'Bitmap Viewer';

    img := TImage.Create(form);
    img.Parent := form;
    img.Align := alClient;
    img.Stretch := True;
    img.Proportional := True;

    bmp := TBitmap.Create;
    try
      bmp.LoadFromFile(wbDataPath + 'image.bmp');
      img.Picture.Assign(bmp);
    finally
      bmp.Free;
    end;

    form.ShowModal;
  finally
    form.Free;
  end;
end;
```

## TFont - Text Fonts

TFont manages font properties for text rendering.

### Properties

| Property | Type | Description |
|----------|------|-------------|
| `Name` | string | Font name (e.g., 'Arial', 'Times New Roman') |
| `Size` | Integer | Font size in points |
| `Style` | TFontStyles | Font styles (set) |
| `Color` | TColor | Text color |
| `Height` | Integer | Font height in pixels |
| `Pitch` | TFontPitch | Font pitch (fpDefault, fpFixed, fpVariable) |
| `Charset` | TFontCharset | Character set |

### Font Style Set

```pascal
TFontStyles = set of (fsBold, fsItalic, fsUnderline, fsStrikeOut);

// Examples:
font.Style := [fsBold];                    // Bold only
font.Style := [fsBold, fsItalic];          // Bold and italic
font.Style := [];                          // Normal (no styles)
font.Style := [fsUnderline, fsStrikeOut];  // Underline and strikeout
```

### Font Example

```pascal
// Configure font
var
  canvas: TCanvas;
begin
  canvas := Form1.Canvas;

  // Set font properties
  canvas.Font.Name := 'Arial';
  canvas.Font.Size := 16;
  canvas.Font.Style := [fsBold, fsItalic];
  canvas.Font.Color := clBlue;

  // Draw text
  canvas.TextOut(10, 10, 'Styled Text');

  // Change style
  canvas.Font.Style := [fsUnderline];
  canvas.Font.Color := clRed;
  canvas.TextOut(10, 40, 'Underlined Red Text');
end;
```

## TPen - Drawing Pen

TPen defines how lines are drawn.

### Properties

| Property | Type | Description |
|----------|------|-------------|
| `Color` | TColor | Pen color |
| `Width` | Integer | Pen width in pixels |
| `Style` | TPenStyle | Line style |
| `Mode` | TPenMode | Drawing mode |

### Pen Style Constants

```pascal
TPenStyle = (
  psSolid,       // Solid line
  psDash,        // Dashed line
  psDot,         // Dotted line
  psDashDot,     // Dash-dot line
  psDashDotDot,  // Dash-dot-dot line
  psClear,       // No line
  psInsideFrame  // Inside frame
);
```

### Pen Mode Constants

```pascal
TPenMode = (
  pmBlack,       // Always black
  pmWhite,       // Always white
  pmNop,         // No operation
  pmNot,         // Inverted screen color
  pmCopy,        // Copy pen color (default)
  pmNotCopy,     // Inverted pen color
  pmMergePenNot, // Merge pen with inverted screen
  pmMaskPenNot,  // Mask pen with inverted screen
  pmMergeNotPen, // Merge inverted pen with screen
  pmMaskNotPen,  // Mask inverted pen with screen
  pmMerge,       // Merge pen with screen
  pmNotMerge,    // Invert merged pen and screen
  pmMask,        // Mask pen with screen
  pmNotMask,     // Invert masked pen and screen
  pmXor,         // XOR pen with screen
  pmNotXor       // Invert XORed pen and screen
);
```

### Pen Example

```pascal
// Draw with different pen styles
var
  canvas: TCanvas;
  y: Integer;
begin
  canvas := Form1.Canvas;
  y := 10;

  // Solid line
  canvas.Pen.Style := psSolid;
  canvas.Pen.Width := 2;
  canvas.Pen.Color := clBlack;
  canvas.MoveTo(10, y);
  canvas.LineTo(200, y);

  // Dashed line
  Inc(y, 20);
  canvas.Pen.Style := psDash;
  canvas.MoveTo(10, y);
  canvas.LineTo(200, y);

  // Dotted line
  Inc(y, 20);
  canvas.Pen.Style := psDot;
  canvas.MoveTo(10, y);
  canvas.LineTo(200, y);

  // Thick colored line
  Inc(y, 20);
  canvas.Pen.Style := psSolid;
  canvas.Pen.Width := 5;
  canvas.Pen.Color := clRed;
  canvas.MoveTo(10, y);
  canvas.LineTo(200, y);
end;
```

## TBrush - Fill Brush

TBrush defines how shapes are filled.

### Properties

| Property | Type | Description |
|----------|------|-------------|
| `Color` | TColor | Fill color |
| `Style` | TBrushStyle | Fill style |

### Brush Style Constants

```pascal
TBrushStyle = (
  bsSolid,       // Solid fill
  bsClear,       // No fill (transparent)
  bsHorizontal,  // Horizontal lines
  bsVertical,    // Vertical lines
  bsFDiagonal,   // Forward diagonal lines
  bsBDiagonal,   // Backward diagonal lines
  bsCross,       // Crosshatch
  bsDiagCross    // Diagonal crosshatch
);
```

### Brush Example

```pascal
// Draw rectangles with different fill styles
var
  canvas: TCanvas;
  x, y: Integer;
begin
  canvas := Form1.Canvas;
  canvas.Pen.Color := clBlack;
  x := 10;
  y := 10;

  // Solid fill
  canvas.Brush.Style := bsSolid;
  canvas.Brush.Color := clYellow;
  canvas.Rectangle(x, y, x + 80, y + 80);

  // Hatched fill
  Inc(x, 100);
  canvas.Brush.Style := bsCross;
  canvas.Brush.Color := clRed;
  canvas.Rectangle(x, y, x + 80, y + 80);

  // No fill (transparent)
  Inc(x, 100);
  canvas.Brush.Style := bsClear;
  canvas.Rectangle(x, y, x + 80, y + 80);
end;
```

## TPicture - Image Container

TPicture is a container for different graphic types (bitmaps, icons, metafiles).

### Properties

| Property | Type | Description |
|----------|------|-------------|
| `Bitmap` | TBitmap | Bitmap graphic |
| `Icon` | TIcon | Icon graphic |
| `Graphic` | TGraphic | Generic graphic |
| `Width` | Integer | Image width |
| `Height` | Integer | Image height |

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `LoadFromFile` | `LoadFromFile(FileName: string)` | Load image from file |
| `SaveToFile` | `SaveToFile(FileName: string)` | Save image to file |
| `Assign` | `Assign(Source: TPersistent)` | Copy from another picture |

### Picture Example

```pascal
// Load and display various image formats
var
  pic: TPicture;
  img: TImage;
begin
  pic := TPicture.Create;
  try
    // Load bitmap
    pic.LoadFromFile('image.bmp');
    AddMessage(Format('Image size: %d x %d', [pic.Width, pic.Height]));

    // Display in TImage
    img.Picture.Assign(pic);
  finally
    pic.Free;
  end;
end;
```

## xEdit Visualization Examples

### Example 1: Draw Record Dependency Graph

```pascal
// Visualize record dependencies
var
  form: TForm;
  bmp: TBitmap;
  img: TImage;
  i, x, y: Integer;
  rec: IwbMainRecord;
  nodeSize: Integer;
begin
  form := TForm.Create(nil);
  try
    form.Width := 800;
    form.Height := 600;
    form.Caption := 'Dependency Graph';

    img := TImage.Create(form);
    img.Parent := form;
    img.Align := alClient;

    bmp := TBitmap.Create;
    try
      bmp.Width := 800;
      bmp.Height := 600;

      // Clear background
      bmp.Canvas.Brush.Color := clWhite;
      bmp.Canvas.FillRect(Rect(0, 0, bmp.Width, bmp.Height));

      nodeSize := 40;
      x := 50;
      y := 50;

      // Draw nodes for each record
      for i := 0 to RecordCount(FileByIndex(0)) - 1 do begin
        rec := RecordByIndex(FileByIndex(0), i);

        // Draw node
        bmp.Canvas.Brush.Color := clLightBlue;
        bmp.Canvas.Pen.Color := clBlack;
        bmp.Canvas.Ellipse(x, y, x + nodeSize, y + nodeSize);

        // Draw label
        bmp.Canvas.Font.Size := 8;
        bmp.Canvas.TextOut(x + 5, y + nodeSize + 5,
          Copy(rec.EditorID, 1, 8));

        // Arrange in grid
        Inc(x, nodeSize + 30);
        if x > 700 then begin
          x := 50;
          Inc(y, nodeSize + 50);
        end;

        if y > 500 then break;
      end;

      img.Picture.Assign(bmp);
    finally
      bmp.Free;
    end;

    form.ShowModal;
  finally
    form.Free;
  end;
end;
```

### Example 2: Color-Coded Record List

```pascal
// Display records with color-coded status
var
  form: TForm;
  listView: TListView;
  paintBox: TPaintBox;
  i: Integer;
  rec: IwbMainRecord;
  color: TColor;
begin
  form := TForm.Create(nil);
  try
    form.Width := 600;
    form.Height := 500;
    form.Caption := 'Record Status';

    // Create paint box for legend
    paintBox := TPaintBox.Create(form);
    paintBox.Parent := form;
    paintBox.Align := alTop;
    paintBox.Height := 60;

    // Draw legend
    paintBox.Canvas.Brush.Color := clGreen;
    paintBox.Canvas.Rectangle(10, 10, 30, 30);
    paintBox.Canvas.TextOut(35, 15, 'Valid');

    paintBox.Canvas.Brush.Color := clYellow;
    paintBox.Canvas.Rectangle(100, 10, 120, 30);
    paintBox.Canvas.TextOut(125, 15, 'Warning');

    paintBox.Canvas.Brush.Color := clRed;
    paintBox.Canvas.Rectangle(200, 10, 220, 30);
    paintBox.Canvas.TextOut(225, 15, 'Error');

    // Create list
    listView := TListView.Create(form);
    listView.Parent := form;
    listView.Align := alClient;
    listView.ViewStyle := vsReport;
    listView.RowSelect := True;

    listView.Columns.Add.Caption := 'EditorID';
    listView.Columns.Add.Caption := 'Status';

    // Add records
    for i := 0 to RecordCount(FileByIndex(0)) - 1 do begin
      rec := RecordByIndex(FileByIndex(0), i);

      // Determine status color
      if rec.IsDeleted then
        color := clRed
      else if rec.IsInitiallyDisabled then
        color := clYellow
      else
        color := clGreen;

      // Add to list (note: actual coloring would need custom drawing)
      with listView.Items.Add do begin
        Caption := rec.EditorID;
        SubItems.Add('Status');
      end;
    end;

    form.ShowModal;
  finally
    form.Free;
  end;
end;
```

### Example 3: Progress Visualization

```pascal
// Visual progress indicator with custom drawing
var
  form: TForm;
  paintBox: TPaintBox;
  progress: Integer;
  total: Integer;

procedure DrawProgress;
var
  w, h, barWidth: Integer;
  pct: Extended;
begin
  w := paintBox.Width;
  h := paintBox.Height;

  // Clear
  paintBox.Canvas.Brush.Color := clWhite;
  paintBox.Canvas.FillRect(Rect(0, 0, w, h));

  // Calculate progress
  pct := progress / total;
  barWidth := Round(w * pct);

  // Draw progress bar
  paintBox.Canvas.Brush.Color := clBlue;
  paintBox.Canvas.FillRect(Rect(0, 0, barWidth, h));

  // Draw border
  paintBox.Canvas.Brush.Style := bsClear;
  paintBox.Canvas.Pen.Color := clBlack;
  paintBox.Canvas.Rectangle(0, 0, w, h);

  // Draw percentage
  paintBox.Canvas.Font.Size := 14;
  paintBox.Canvas.Font.Style := [fsBold];
  paintBox.Canvas.TextOut(10, 10,
    Format('%d%% (%d / %d)', [Round(pct * 100), progress, total]));
end;

begin
  form := TForm.Create(nil);
  try
    form.Width := 500;
    form.Height := 150;
    form.Caption := 'Processing';

    paintBox := TPaintBox.Create(form);
    paintBox.Parent := form;
    paintBox.Left := 10;
    paintBox.Top := 30;
    paintBox.Width := form.ClientWidth - 20;
    paintBox.Height := 60;

    form.Show;

    total := RecordCount(FileByIndex(0));

    for progress := 0 to total - 1 do begin
      // Process record...

      // Update display
      if (progress mod 10) = 0 then begin
        DrawProgress;
        Application.ProcessMessages;
      end;
    end;

    ShowMessage('Processing complete!');
  finally
    form.Free;
  end;
end;
```

---

[← Back to Standard Library Overview](stdlib_home.md) | [Next: Data Structures →](stdlib_data.md)

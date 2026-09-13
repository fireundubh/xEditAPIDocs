# Graphics & Drawing Reference

Graphics classes for drawing, images, fonts, colors, and visual elements in xEdit scripts.

**Units:** Graphics

[← Back to Standard Library Overview](stdlib_home.md)

## Table of Contents

- [Colors](#colors)
- [TCanvas - Drawing Surface](#tcanvas---drawing-surface)
- [TBitmap - Bitmap Images](#tbitmap---bitmap-images)
- [TFont - Text Fonts](#tfont---text-fonts)
- [TPen - Drawing Pen](#tpen---drawing-pen)
- [TBrush - Fill Brush](#tbrush---fill-brush)
- [TPicture - Image Container](#tpicture---image-container)
- [xEdit Visualization Examples](#xedit-visualization-examples)

## Colors

`RGB`, `ColorToRGB`, `GetRValue`, `GetGValue`, and `GetBValue` are **not** registered. Build a `TColor` as `$00BBGGRR` (blue in the high byte of the low word, red in the low byte).

```pascal
color := $004080FF;  // R=255, G=128, B=64
```

Registered named colors include `clBlack`…`clWhite` and `clWebLightBlue` (there is no `clLightBlue`).

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

Use the registered `cl*` names. `COLOR_SCROLLBAR` and the other `COLOR_*` identifiers are **not** registered.

```pascal
clScrollBar, clBackground, clActiveCaption, clInactiveCaption,
clMenu, clWindow, clWindowFrame, clMenuText, clWindowText,
clCaptionText, clActiveBorder, clInactiveBorder, clAppWorkSpace,
clHighlight, clHighlightText, clBtnFace, clBtnShadow, clGrayText,
clBtnText, clInactiveCaptionText, clBtnHighlight, cl3DDkShadow,
cl3DLight, clInfoText, clInfoBk, clHotLight,
clGradientActiveCaption, clGradientInactiveCaption,
clMenuHighlight, clMenuBar
```

### Color Example

```pascal
var
  bmp: TBitmap;
  color: TColor;
begin
  bmp := TBitmap.Create;
  try
    bmp.Width := 100;
    bmp.Height := 100;
    color := $004080FF;  // orange: R=255 G=128 B=64
    bmp.Canvas.Brush.Color := color;
    bmp.Canvas.Pen.Color := clBlack;
    bmp.Canvas.Rectangle(0, 0, 100, 100);
  finally
    bmp.Free;
  end;
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

`TCanvas.Pixels` is not registered. Fill areas with `FillRect` / `Rectangle` instead.

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
// Draw on a bitmap canvas (no custom form class)
var
  bmp: TBitmap;
  canvas: TCanvas;
begin
  bmp := TBitmap.Create;
  try
    bmp.Width := 240;
    bmp.Height := 180;
    canvas := bmp.Canvas;

    canvas.Pen.Color := clBlack;
    canvas.Pen.Width := 2;
    canvas.Brush.Color := clYellow;

    canvas.Rectangle(10, 10, 100, 100);
    canvas.Ellipse(120, 10, 210, 100);

    canvas.MoveTo(10, 120);
    canvas.LineTo(210, 120);

    canvas.Font.Size := 14;
    canvas.Font.Style := [fsBold];
    canvas.TextOut(10, 140, 'Hello World');
  finally
    bmp.Free;
  end;
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

### Bitmap Example

```pascal
// Create and manipulate bitmap
var
  bmp: TBitmap;
begin
  bmp := TBitmap.Create;
  try
    // Create blank bitmap
    bmp.Width := 200;
    bmp.Height := 200;
    bmp.PixelFormat := pf24bit;

    bmp.Canvas.Brush.Color := $00808080;
    bmp.Canvas.FillRect(Rect(0, 0, bmp.Width, bmp.Height));

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
  bmp: TBitmap;
  canvas: TCanvas;
begin
  bmp := TBitmap.Create;
  try
    bmp.Width := 300;
    bmp.Height := 80;
    canvas := bmp.Canvas;

    canvas.Font.Name := 'Arial';
    canvas.Font.Size := 16;
    canvas.Font.Style := [fsBold, fsItalic];
    canvas.Font.Color := clBlue;
    canvas.TextOut(10, 10, 'Styled Text');

    canvas.Font.Style := [fsUnderline];
    canvas.Font.Color := clRed;
    canvas.TextOut(10, 40, 'Underlined Red Text');
  finally
    bmp.Free;
  end;
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
  bmp: TBitmap;
  canvas: TCanvas;
  y: Integer;
begin
  bmp := TBitmap.Create;
  try
    bmp.Width := 220;
    bmp.Height := 100;
    canvas := bmp.Canvas;
    y := 10;

    canvas.Pen.Style := psSolid;
    canvas.Pen.Width := 2;
    canvas.Pen.Color := clBlack;
    canvas.MoveTo(10, y);
    canvas.LineTo(200, y);

    Inc(y, 20);
    canvas.Pen.Style := psDash;
    canvas.MoveTo(10, y);
    canvas.LineTo(200, y);

    Inc(y, 20);
    canvas.Pen.Style := psDot;
    canvas.MoveTo(10, y);
    canvas.LineTo(200, y);

    Inc(y, 20);
    canvas.Pen.Style := psSolid;
    canvas.Pen.Width := 5;
    canvas.Pen.Color := clRed;
    canvas.MoveTo(10, y);
    canvas.LineTo(200, y);
  finally
    bmp.Free;
  end;
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
  bmp: TBitmap;
  canvas: TCanvas;
  x, y: Integer;
begin
  bmp := TBitmap.Create;
  try
    bmp.Width := 320;
    bmp.Height := 100;
    canvas := bmp.Canvas;
    canvas.Pen.Color := clBlack;
    x := 10;
    y := 10;

    canvas.Brush.Style := bsSolid;
    canvas.Brush.Color := clYellow;
    canvas.Rectangle(x, y, x + 80, y + 80);

    Inc(x, 100);
    canvas.Brush.Style := bsCross;
    canvas.Brush.Color := clRed;
    canvas.Rectangle(x, y, x + 80, y + 80);

    Inc(x, 100);
    canvas.Brush.Style := bsClear;
    canvas.Rectangle(x, y, x + 80, y + 80);
  finally
    bmp.Free;
  end;
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
// Load an image and report size
var
  pic: TPicture;
begin
  pic := TPicture.Create;
  try
    pic.LoadFromFile(wbDataPath + 'image.bmp');
    AddMessage(Format('Image size: %d x %d', [pic.Width, pic.Height]));
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
        bmp.Canvas.Brush.Color := clWebLightBlue;
        bmp.Canvas.Pen.Color := clBlack;
        bmp.Canvas.Ellipse(x, y, x + nodeSize, y + nodeSize);

        // Draw label
        bmp.Canvas.Font.Size := 8;
        bmp.Canvas.TextOut(x + 5, y + nodeSize + 5,
          Copy(EditorID(rec), 1, 8));

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
  status: string;
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

      if GetIsDeleted(rec) then
        status := 'Deleted'
      else if GetIsInitiallyDisabled(rec) then
        status := 'Disabled'
      else
        status := 'Valid';

      with listView.Items.Add do begin
        Caption := EditorID(rec);
        SubItems.Add(status);
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

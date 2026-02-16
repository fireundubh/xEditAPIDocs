# Standard Library Reference for xEdit Scripts

This reference documents the standard library functions and classes available to xEdit scripts through the JvInterpreter adapter configuration.

## Quick Navigation

### By Functionality
- **[Core Functions](stdlib_core.md)** - Strings, numbers, arrays, conversions, variants
- **[File & Path Operations](stdlib_files.md)** - File I/O, path manipulation, directory operations
- **[Date & Time](stdlib_datetime.md)** - Date/time creation, formatting, calculations
- **[Mathematics](stdlib_math.md)** - Advanced math, trigonometry, logarithms, financial functions
- **[User Interface](stdlib_ui.md)** - Forms, dialogs, controls, menus
- **[Graphics & Drawing](stdlib_graphics.md)** - Canvas, bitmaps, fonts, colors
- **[Data Structures](stdlib_data.md)** - Lists, strings, streams, collections

### By Common Task
| Task | Functions | Page |
|------|-----------|------|
| Format text with values | `Format()`, `FormatFloat()`, `FormatDateTime()` | [Core](stdlib_core.md#string-formatting) |
| Read/write files | `TStringList`, `TFileStream`, `TMemoryStream` | [Files](stdlib_files.md#streams) |
| Build file paths | `ExtractFilePath()`, `ChangeFileExt()`, `IncludeTrailingPathDelimiter()` | [Files](stdlib_files.md#path-functions) |
| Show messages to user | `ShowMessage()`, `MessageDlg()`, `InputBox()` | [UI](stdlib_ui.md#dialogs) |
| Create dynamic forms | `TForm`, `TButton`, `TEdit`, `TMemo` | [UI](stdlib_ui.md#creating-forms) |
| Math calculations | `Power()`, `Sqrt()`, `Sin()`, `Cos()`, `Max()`, `Min()` | [Math](stdlib_math.md) |
| Work with dates | `Now()`, `FormatDateTime()`, `IncMonth()` | [DateTime](stdlib_datetime.md) |
| Process strings | `Pos()`, `Copy()`, `Trim()`, `UpperCase()`, `AnsiCompareText()` | [Core](stdlib_core.md#string-functions) |

## Configuration Overview

xEdit scripts use the following adapter configuration for the standard JvInterpreter library:

```pascal
JvInterpreterFm.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_System.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_SysUtils.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_Classes.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_Dialogs.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_Windows.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_Graphics.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_Controls.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_Buttons.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_StdCtrls.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_ComCtrls.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_ExtCtrls.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_Forms.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_Menus.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
JvInterpreter_Math.RegisterJvInterpreterAdapter(GlobalJvInterpreterAdapter);
```

### Key Features

✅ **Math-Enhanced** - Full Math unit support (trigonometry, logarithms, financial functions)
✅ **GUI-Complete** - All VCL controls for building forms
✅ **No Database** - No database dependencies (smaller, simpler)
✅ **Form Runner** - Load and execute forms from .pas/.dfm files
✅ **File I/O** - Complete file and directory operations
✅ **String Processing** - Extensive string manipulation functions
✅ **Date/Time** - Full date/time support with formatting
✅ **Graphics** - Drawing, bitmaps, icons, fonts
✅ **Dialogs** - Message boxes, input dialogs, file dialogs

This configuration provides a **GUI-focused, non-database** adapter set with **enhanced math capabilities**.

## Quick Reference Tables

### Most Common Functions

#### String Operations
| Function | Purpose | Example |
|----------|---------|---------|
| `Format(fmt, args)` | Format string with values | `Format('Found %d records', [count])` |
| `IntToStr(n)` | Integer to string | `IntToStr(123)` → `'123'` |
| `StrToInt(s)` | String to integer | `StrToInt('123')` → `123` |
| `UpperCase(s)` | Convert to uppercase | `UpperCase('hello')` → `'HELLO'` |
| `LowerCase(s)` | Convert to lowercase | `LowerCase('HELLO')` → `'hello'` |
| `Trim(s)` | Remove whitespace | `Trim('  text  ')` → `'text'` |
| `Pos(sub, s)` | Find substring | `Pos('lo', 'hello')` → `4` |
| `Copy(s, idx, len)` | Extract substring | `Copy('hello', 2, 3)` → `'ell'` |

#### File Operations
| Function | Purpose | Example |
|----------|---------|---------|
| `FileExists(path)` | Check if file exists | `if FileExists(fn) then ...` |
| `ExtractFilePath(path)` | Get directory path | `ExtractFilePath('C:\Dir\file.txt')` → `'C:\Dir\'` |
| `ExtractFileName(path)` | Get filename | `ExtractFileName('C:\Dir\file.txt')` → `'file.txt'` |
| `ExtractFileExt(path)` | Get extension | `ExtractFileExt('file.txt')` → `'.txt'` |
| `ChangeFileExt(path, ext)` | Replace extension | `ChangeFileExt('file.txt', '.esp')` |

#### Math Functions
| Function | Purpose | Example |
|----------|---------|---------|
| `Abs(x)` | Absolute value | `Abs(-5)` → `5` |
| `Max(a, b)` | Maximum of two | `Max(10, 20)` → `20` |
| `Min(a, b)` | Minimum of two | `Min(10, 20)` → `10` |
| `Power(base, exp)` | Power | `Power(2, 10)` → `1024` |
| `Sqrt(x)` | Square root | `Sqrt(144)` → `12` |
| `Round(x)` | Round to integer | `Round(3.7)` → `4` |
| `Ceil(x)` | Round up | `Ceil(3.1)` → `4` |
| `Floor(x)` | Round down | `Floor(3.9)` → `3` |

#### Date/Time Functions
| Function | Purpose | Example |
|----------|---------|---------|
| `Now()` | Current date/time | `dt := Now();` |
| `Date()` | Current date | `d := Date();` |
| `FormatDateTime(fmt, dt)` | Format date/time | `FormatDateTime('yyyy-mm-dd', Now())` |
| `EncodeDate(y, m, d)` | Create date | `EncodeDate(2024, 12, 25)` |
| `DayOfWeek(dt)` | Day of week | `DayOfWeek(Now())` → `1..7` |

### xEdit Integration Examples

#### Example 1: Format Record Information
```pascal
// Display formatted record details
var
  rec: IwbMainRecord;
  msg: string;
begin
  rec := e;  // current element
  msg := Format('Record: %s [%s]'#13#10'FormID: %s'#13#10'EditorID: %s', [
    rec.Name,
    rec.Signature,
    IntToHex(rec.FormID, 8),
    rec.EditorID
  ]);
  ShowMessage(msg);
end;
```

#### Example 2: Build Output Path
```pascal
// Create output file path
var
  basePath, fileName, outputPath: string;
begin
  basePath := wbDataPath;
  fileName := ChangeFileExt(ExtractFileName(GetFileName(e)), '.txt');
  outputPath := IncludeTrailingPathDelimiter(basePath) + 'Output\' + fileName;

  if not DirectoryExists(ExtractFilePath(outputPath)) then
    ForceDirectories(ExtractFilePath(outputPath));

  AddMessage('Writing to: ' + outputPath);
end;
```

#### Example 3: Process Records with Progress
```pascal
// Process records with timestamp
var
  i, total: Integer;
  rec: IwbMainRecord;
  startTime: TDateTime;
  elapsed: string;
begin
  startTime := Now();
  total := FileByIndex(0).RecordCount;

  for i := 0 to total - 1 do begin
    rec := FileByIndex(0).Records[i];
    // Process record...

    if (i mod 100) = 0 then begin
      elapsed := FormatDateTime('nn:ss', Now() - startTime);
      AddMessage(Format('Progress: %d/%d (%s elapsed)', [i, total, elapsed]));
    end;
  end;
end;
```

#### Example 4: Validate User Input
```pascal
// Get validated number from user
var
  input: string;
  value: Integer;
begin
  if InputQuery('Enter Value', 'Enter a number (1-100):', input) then begin
    if not TryStrToInt(input, value) then begin
      MessageDlg('Invalid number entered.', mtError, [mbOK], 0);
      Exit;
    end;

    if not InRange(value, 1, 100) then begin
      MessageDlg('Value must be between 1 and 100.', mtWarning, [mbOK], 0);
      Exit;
    end;

    AddMessage(Format('User entered: %d', [value]));
  end;
end;
```

## Statistics

### Available Functions and Classes

**Functions:** 240+ standard library functions
- System: 40+
- SysUtils: 163
- Math: 60+
- Dialogs: 10+
- Form runner: 4
- Windows API: 20+

**Classes:** 50+ VCL classes
- **Base:** TObject, TPersistent, TComponent
- **Collections:** TList, TStrings, TStringList, TCollection
- **Streams:** TStream, TFileStream, TMemoryStream
- **Graphics:** TCanvas, TBitmap, TFont, TPen, TBrush
- **Controls:** TControl, TWinControl, TForm
- **Standard:** TLabel, TEdit, TMemo, TButton, TCheckBox, TListBox, TComboBox
- **Common:** TTreeView, TListView, TProgressBar, TStatusBar, TPageControl
- **Extended:** TPanel, TImage, TTimer, TSplitter
- **Dialogs:** TOpenDialog, TSaveDialog, TColorDialog, TFontDialog
- **Menus:** TMainMenu, TPopupMenu, TMenuItem
- **Application:** TApplication, TScreen

## Related Documentation

- [Core Functions Reference](stdlib_core.md) - String, number, array, and conversion functions
- [File Operations Reference](stdlib_files.md) - File I/O and path manipulation
- [Date/Time Reference](stdlib_datetime.md) - Date and time functions
- [Math Reference](stdlib_math.md) - Advanced mathematics
- [UI Components Reference](stdlib_ui.md) - Forms, dialogs, and controls
- [Graphics Reference](stdlib_graphics.md) - Drawing and images
- [Data Structures Reference](stdlib_data.md) - Lists, strings, and streams
- [Constants Reference](CONSTANTS.md) - All available constants
- [Glossary](GLOSSARY.md) - Term definitions

# Standard Library Reference for xEdit Scripts

This reference documents the standard library functions and classes available to xEdit scripts.

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
| Build file paths | `ExtractFilePath()`, `ChangeFileExt()`, `IncludeTrailingBackslash()` | [Files](stdlib_files.md#path-functions) |
| Show messages to user | `ShowMessage()`, `MessageDlg()`, `InputBox()` | [UI](stdlib_ui.md#dialogs) |
| Create dynamic forms | `TForm`, `TButton`, `TEdit`, `TMemo` | [UI](stdlib_ui.md#creating-forms) |
| Math calculations | `Power()`, `Sqrt()`, `Sin()`, `Cos()`, `Max()`, `Min()` | [Math](stdlib_math.md) |
| Work with dates | `Now()`, `FormatDateTime()`, `IncMonth()` | [DateTime](stdlib_datetime.md) |
| Process strings | `Pos()`, `Copy()`, `Trim()`, `UpperCase()`, `AnsiCompareText()` | [Core](stdlib_core.md#string-functions) |

## Key Features

- **Math** — trigonometry, logarithms, `Power`/`Floor`/`Ceil`, integer `Max`/`Min`, SLN/SYD depreciation (not the full Delphi Math unit)
- **GUI** — VCL controls, dialogs, and the JvInterpreter form runner
- **Files** — SysUtils paths, streams, `FindFirst`/`FindNext`
- **Date/time** — SysUtils only (`EncodeDate`/`EncodeTime`/`IncMonth`/`DayOfWeek`). DateUtils is not registered.
- **Graphics** — `TCanvas`/`TBitmap`/`TFont` (no `RGB`/`Pixels`/`Line`)

## Quick Reference Tables

**Contents:**
- [Most Common Functions](#most-common-functions)
  - [String Operations](#string-operations)
  - [File Operations](#file-operations)
  - [Math Functions](#math-functions)
  - [Date/Time Functions](#datetime-functions)
- [xEdit Integration Examples](#xedit-integration-examples)
  - [Example 1: Format Record Information](#example-1-format-record-information)
  - [Example 2: Build Output Path](#example-2-build-output-path)
  - [Example 3: Process Records with Progress](#example-3-process-records-with-progress)
  - [Example 4: Validate User Input](#example-4-validate-user-input)

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
| `Max(a, b)` | Maximum of two integers | `Max(10, 20)` → `20` |
| `Min(a, b)` | Minimum of two integers | `Min(10, 20)` → `10` |
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
    Name(rec),
    Signature(rec),
    IntToHex(FormID(rec), 8),
    EditorID(rec)
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
  outputPath := IncludeTrailingBackslash(basePath) + 'Output\' + fileName;

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
  total := RecordCount(FileByIndex(0));

  for i := 0 to total - 1 do begin
    rec := RecordByIndex(FileByIndex(0), i);
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
    value := StrToIntDef(input, -1);
    if value = -1 then begin
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

**Functions:** hundreds of registered stdlib functions (not the full Delphi RTL)
- System, SysUtils, Math (integer `Max`/`Min`; no DateUtils)
- Dialogs, Forms (`Application`/`Screen` are 0-arg functions)
- Windows API helpers (`CopyFile`, `Sleep`, …)

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
- [Constants Reference](Constants.md) - All available constants
- [Glossary](Glossary.md) - Term definitions

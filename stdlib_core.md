# Core Functions Reference

Core functions for string manipulation, number conversion, arrays, variants, and basic operations.

**Units:** System, SysUtils

[← Back to Standard Library Overview](stdlib_home.md)

## Table of Contents

- [String Functions](#string-functions)
- [String Formatting](#string-formatting)
- [Number Conversion](#number-conversion)
- [Character Functions](#character-functions)
- [Array Functions](#array-functions)
- [Variant Functions](#variant-functions)
- [Basic Math](#basic-math)
- [Command-Line](#command-line)
- [Random Numbers](#random-numbers)

## String Functions

### Basic String Operations

| Function | Signature | Description |
|----------|-----------|-------------|
| `Length` | `Length(S: string): Integer` | Get string length |
| `Copy` | `Copy(S: string, Index, Count: Integer): string` | Extract substring starting at Index (1-based) |
| `Pos` | `Pos(Substr, S: string): Integer` | Find substring position (1-based, 0 = not found) |
| `Delete` | `Delete(var S: string, Index, Count: Integer)` | Delete substring (modifies S) |
| `Insert` | `Insert(Source: string, var S: string, Index: Integer)` | Insert substring (modifies S) |
| `SetLength` | `SetLength(var S: string, NewLength: Integer)` | Resize string |

### Case Conversion

| Function | Signature | Description |
|----------|-----------|-------------|
| `UpperCase` | `UpperCase(S: string): string` | Convert to uppercase |
| `LowerCase` | `LowerCase(S: string): string` | Convert to lowercase |
| `AnsiUpperCase` | `AnsiUpperCase(S: string): string` | ANSI uppercase (locale-aware) |
| `AnsiLowerCase` | `AnsiLowerCase(S: string): string` | ANSI lowercase (locale-aware) |
| `UpCase` | `UpCase(Ch: Char): Char` | Convert single character to uppercase |

### Trimming and Whitespace

| Function | Signature | Description |
|----------|-----------|-------------|
| `Trim` | `Trim(S: string): string` | Remove leading and trailing whitespace |
| `TrimLeft` | `TrimLeft(S: string): string` | Remove leading whitespace |
| `TrimRight` | `TrimRight(S: string): string` | Remove trailing whitespace |

### String Comparison

| Function | Signature | Description |
|----------|-----------|-------------|
| `CompareStr` | `CompareStr(S1, S2: string): Integer` | Case-sensitive comparison (-1, 0, 1) |
| `CompareText` | `CompareText(S1, S2: string): Integer` | Case-insensitive comparison (-1, 0, 1) |
| `AnsiCompareStr` | `AnsiCompareStr(S1, S2: string): Integer` | ANSI case-sensitive comparison |
| `AnsiCompareText` | `AnsiCompareText(S1, S2: string): Integer` | ANSI case-insensitive comparison |
| `AnsiPos` | `AnsiPos(Substr, S: string): Integer` | ANSI substring search |

### String Utilities

| Function | Signature | Description |
|----------|-----------|-------------|
| `QuotedStr` | `QuotedStr(S: string): string` | Wrap string in single quotes |
| `IsValidIdent` | `IsValidIdent(Ident: string): Boolean` | Check if valid Pascal identifier |
| `IsDelimiter` | `IsDelimiter(Delimiters, S: string, Index: Integer): Boolean` | Check if character at index is delimiter |
| `LastDelimiter` | `LastDelimiter(Delimiters, S: string): Integer` | Find last occurrence of any delimiter |

### xEdit Integration Examples

#### Extract Record Type from Signature
```pascal
// Parse record signature
var
  rec: IwbMainRecord;
  sig, recType: string;
begin
  rec := e;
  sig := rec.Signature;

  // Extract first two characters
  recType := Copy(sig, 1, 2);

  if CompareText(recType, 'NP') = 0 then
    AddMessage('Found NPC record')
  else if CompareText(recType, 'WE') = 0 then
    AddMessage('Found WEAP record');
end;
```

#### Clean and Validate EditorID
```pascal
// Sanitize EditorID input
function SanitizeEditorID(const edid: string): string;
var
  clean: string;
begin
  clean := Trim(edid);
  clean := UpperCase(clean);

  // Remove invalid characters
  if not IsValidIdent(clean) then begin
    AddMessage('Warning: EditorID contains invalid characters: ' + edid);
    // Strip invalid chars here...
  end;

  Result := clean;
end;
```

#### Search for Substrings in Element Values
```pascal
// Find elements containing search term
var
  i: Integer;
  el: IwbElement;
  value, searchTerm: string;
begin
  searchTerm := 'Daedric';

  for i := 0 to ElementCount(e) - 1 do begin
    el := ElementByIndex(e, i);
    value := GetEditValue(el);

    if Pos(searchTerm, value) > 0 then
      AddMessage(Format('Found in %s: %s', [Name(el), value]));
  end;
end;
```

## String Formatting

### Format Function

**Signature:** `Format(Format: string, Args: array of const): string`

Format strings using printf-style specifiers. This is one of the most useful functions for creating readable output.

#### Format Specifiers

| Specifier | Type | Description | Example |
|-----------|------|-------------|---------|
| `%s` | String | String value | `Format('Name: %s', ['John'])` → `'Name: John'` |
| `%d` | Integer | Decimal integer | `Format('Count: %d', [42])` → `'Count: 42'` |
| `%x` | Integer | Hexadecimal (lowercase) | `Format('ID: %x', [255])` → `'ID: ff'` |
| `%X` | Integer | Hexadecimal (uppercase) | `Format('ID: %X', [255])` → `'ID: FF'` |
| `%f` | Float | Fixed-point | `Format('Value: %f', [3.14])` → `'Value: 3.14'` |
| `%g` | Float | Shortest representation | `Format('%g', [0.0001])` → `'0.0001'` |
| `%e` | Float | Scientific notation | `Format('%e', [1234.5])` → `'1.2345e+03'` |
| `%p` | Pointer | Pointer address | `Format('%p', [ptr])` |
| `%%` | Literal | Percent sign | `Format('100%% complete', [])` → `'100% complete'` |

#### Width and Precision

```pascal
Format('%5d', [42])        // '   42' (width 5, right-aligned)
Format('%-5d', [42])       // '42   ' (width 5, left-aligned)
Format('%05d', [42])       // '00042' (width 5, zero-padded)
Format('%8.2f', [3.14159]) // '    3.14' (width 8, 2 decimals)
Format('%.2f', [3.14159])  // '3.14' (2 decimals)
```

### xEdit Formatting Examples

#### Format Record Information
```pascal
// Display record details with consistent formatting
var
  rec: IwbMainRecord;
  formID: Cardinal;
  msg: string;
begin
  rec := e;
  formID := rec.FormID;

  msg := Format(
    'Record Information:'#13#10 +
    '  Name:     %s'#13#10 +
    '  Signature: %s'#13#10 +
    '  FormID:   %s (0x%08X)'#13#10 +
    '  EditorID: %s'#13#10 +
    '  File:     %s',
    [
      rec.Name,
      rec.Signature,
      IntToHex(formID, 8),
      formID,
      rec.EditorID,
      GetFileName(GetFile(rec))
    ]
  );

  AddMessage(msg);
end;
```

#### Format Progress Messages
```pascal
// Show processing progress
var
  i, total, pct: Integer;
begin
  total := RecordCount(f);

  for i := 0 to total - 1 do begin
    // Process record...

    if (i mod 100) = 0 then begin
      pct := Round((i / total) * 100);
      AddMessage(Format('Processing: %d/%d (%d%%)', [i, total, pct]));
    end;
  end;
end;
```

#### Format Table Output
```pascal
// Create aligned table output
var
  records: TStringList;
  i: Integer;
  rec: IwbMainRecord;
begin
  records := TStringList.Create;
  try
    AddMessage('EditorID                      FormID    Signature');
    AddMessage('---------------------------------------------------');

    for i := 0 to RecordCount(f) - 1 do begin
      rec := RecordByIndex(f, i);
      // %-30s = left-aligned, width 30
      // %8s = right-aligned, width 8
      AddMessage(Format('%-30s  %8s  %s', [
        rec.EditorID,
        IntToHex(rec.FormID, 8),
        rec.Signature
      ]));
    end;
  finally
    records.Free;
  end;
end;
```

### Other Formatting Functions

| Function | Purpose | Example |
|----------|---------|---------|
| `FmtStr(var Result, Format, Args)` | Format into existing string | `FmtStr(s, '%d items', [count])` |

## Number Conversion

### Integer Conversion

| Function | Signature | Description |
|----------|-----------|-------------|
| `IntToStr` | `IntToStr(Value: Integer): string` | Integer to string |
| `IntToHex` | `IntToHex(Value: Integer, Digits: Integer): string` | Integer to hex (uppercase) |
| `StrToInt` | `StrToInt(S: string): Integer` | String to integer (raises exception on error) |
| `StrToIntDef` | `StrToIntDef(S: string, Default: Integer): Integer` | String to integer (returns default on error) |
| `TryStrToInt` | `TryStrToInt(S: string, var Value: Integer): Boolean` | Safe string to integer conversion |

### Float Conversion

| Function | Signature | Description |
|----------|-----------|-------------|
| `FloatToStr` | `FloatToStr(Value: Extended): string` | Float to string |
| `FloatToStrF` | `FloatToStrF(Value: Extended, Format: TFloatFormat, Precision, Digits: Integer): string` | Float to string with format |
| `StrToFloat` | `StrToFloat(S: string): Extended` | String to float (raises exception) |
| `TryStrToFloat` | `TryStrToFloat(S: string, var Value: Extended): Boolean` | Safe string to float conversion |
| `FormatFloat` | `FormatFloat(Format: string, Value: Extended): string` | Custom float formatting |

### Currency Conversion

| Function | Signature | Description |
|----------|-----------|-------------|
| `CurrToStr` | `CurrToStr(Value: Currency): string` | Currency to string |
| `StrToCurr` | `StrToCurr(S: string): Currency` | String to currency |

### xEdit Conversion Examples

#### Safe FormID Parsing
```pascal
// Parse FormID from user input
var
  input: string;
  formID: Integer;
  rec: IwbMainRecord;
begin
  if InputQuery('Enter FormID', 'FormID (hex):', input) then begin
    // Remove '0x' prefix if present
    if Copy(input, 1, 2) = '0x' then
      input := Copy(input, 3, Length(input) - 2);

    // Try to parse as hex
    if TryStrToInt('$' + input, formID) then begin
      rec := RecordByFormID(FileByIndex(0), formID, True);
      if Assigned(rec) then
        AddMessage('Found: ' + rec.EditorID)
      else
        AddMessage('Record not found');
    end else
      MessageDlg('Invalid FormID format', mtError, [mbOK], 0);
  end;
end;
```

#### Parse Numeric Element Values
```pascal
// Get numeric value safely
function GetElementValueAsFloat(el: IwbElement; default: Extended): Extended;
var
  s: string;
  value: Extended;
begin
  s := GetEditValue(el);

  if TryStrToFloat(s, value) then
    Result := value
  else begin
    AddMessage('Warning: Could not parse as float: ' + s);
    Result := default;
  end;
end;
```

## Character Functions

| Function | Signature | Description |
|----------|-----------|-------------|
| `Chr` | `Chr(Value: Integer): Char` | Convert ASCII code to character |
| `Ord` | `Ord(Value: Char): Integer` | Convert character to ASCII code |
| `UpCase` | `UpCase(Ch: Char): Char` | Convert character to uppercase |

### Example: Build Custom String
```pascal
// Build string with special characters
var
  s: string;
begin
  s := 'Line 1' + Chr(13) + Chr(10) + 'Line 2';  // CRLF
  // Or use: s := 'Line 1'#13#10'Line 2';
  AddMessage(s);
end;
```

## Array Functions

| Function | Signature | Description |
|----------|-----------|-------------|
| `Length` | `Length(A: array): Integer` | Get array length |
| `SetLength` | `SetLength(var A: array, NewLength: Integer)` | Resize dynamic array |
| `High` | `High(A: array): Integer` | Highest index (Length - 1) |
| `Low` | `Low(A: array): Integer` | Lowest index (usually 0) |
| `DeleteFromArray` | `DeleteFromArray(A: Variant, Index: Integer): Variant` | Remove element |
| `InsertIntoArray` | `InsertIntoArray(A: Variant, Index: Integer, Value: Variant): Variant` | Insert element |

### Array Example
```pascal
var
  arr: array of string;
  i: Integer;
begin
  SetLength(arr, 3);
  arr[0] := 'First';
  arr[1] := 'Second';
  arr[2] := 'Third';

  AddMessage(Format('Array has %d elements', [Length(arr)]));

  for i := Low(arr) to High(arr) do
    AddMessage(Format('  [%d] = %s', [i, arr[i]]));
end;
```

## Variant Functions

Variants are flexible types that can hold different kinds of values.

| Function | Signature | Description |
|----------|-----------|-------------|
| `VarType` | `VarType(V: Variant): Integer` | Get variant type code |
| `VarAsType` | `VarAsType(V: Variant, VarType: Integer): Variant` | Convert variant type |
| `VarIsEmpty` | `VarIsEmpty(V: Variant): Boolean` | Check if empty (uninitialized) |
| `VarIsNull` | `VarIsNull(V: Variant): Boolean` | Check if null |
| `VarToStr` | `VarToStr(V: Variant): string` | Convert to string |

### Variant Array Functions

| Function | Signature | Description |
|----------|-----------|-------------|
| `VarArrayCreate` | `VarArrayCreate(Bounds, VarType: Integer): Variant` | Create variant array |
| `VarArrayOf` | `VarArrayOf(Values: array of const): Variant` | Create from values |
| `VarIsArray` | `VarIsArray(V: Variant): Boolean` | Check if array |
| `VarArrayDimCount` | `VarArrayDimCount(A: Variant): Integer` | Number of dimensions |
| `VarArrayLowBound` | `VarArrayLowBound(A: Variant, Dim: Integer): Integer` | Lower bound |
| `VarArrayHighBound` | `VarArrayHighBound(A: Variant, Dim: Integer): Integer` | Upper bound |

### Variant Example
```pascal
var
  v: Variant;
begin
  v := 42;
  AddMessage('Type: ' + IntToStr(VarType(v)));  // varInteger

  v := 'Hello';
  AddMessage('Type: ' + IntToStr(VarType(v)));  // varString

  if VarIsEmpty(v) then
    AddMessage('Variant is empty')
  else
    AddMessage('Variant contains: ' + VarToStr(v));
end;
```

## Basic Math

These basic math functions are in the System unit. For advanced math, see [Math Reference](stdlib_math.md).

| Function | Signature | Description |
|----------|-----------|-------------|
| `Abs` | `Abs(X): Variant` | Absolute value |
| `Round` | `Round(X: Extended): Integer` | Round to nearest integer |
| `Trunc` | `Trunc(X: Extended): Integer` | Truncate (remove decimals) |
| `Sqr` | `Sqr(X: Extended): Extended` | Square (X²) |
| `Sqrt` | `Sqrt(X: Extended): Extended` | Square root (√X) |
| `Exp` | `Exp(X: Extended): Extended` | Exponential (e^X) |
| `Ln` | `Ln(X: Extended): Extended` | Natural logarithm |
| `Sin` | `Sin(X: Extended): Extended` | Sine (radians) |
| `Cos` | `Cos(X: Extended): Extended` | Cosine (radians) |
| `Tan` | `Tan(X: Extended): Extended` | Tangent (radians) |
| `ArcTan` | `ArcTan(X: Extended): Extended` | Arctangent (radians) |

### Example: Calculate Distance
```pascal
// Calculate 3D distance between two points
function Distance3D(x1, y1, z1, x2, y2, z2: Extended): Extended;
var
  dx, dy, dz: Extended;
begin
  dx := x2 - x1;
  dy := y2 - y1;
  dz := z2 - z1;
  Result := Sqrt(Sqr(dx) + Sqr(dy) + Sqr(dz));
end;
```

## Command-Line

| Function | Signature | Description |
|----------|-----------|-------------|
| `ParamCount` | `ParamCount(): Integer` | Number of command-line parameters |
| `ParamStr` | `ParamStr(Index: Integer): string` | Get parameter (0 = program path) |

### Example: Check for Command-Line Arguments
```pascal
var
  i: Integer;
begin
  AddMessage(Format('Program: %s', [ParamStr(0)]));
  AddMessage(Format('Arguments: %d', [ParamCount()]));

  for i := 1 to ParamCount() do
    AddMessage(Format('  Arg %d: %s', [i, ParamStr(i)]));
end;
```

## Random Numbers

| Function | Signature | Description |
|----------|-----------|-------------|
| `Randomize` | `Randomize()` | Initialize random number generator (call once at start) |
| `Random` | `Random(): Extended` | Random float in [0..1) |
| `Random` | `Random(Range: Integer): Integer` | Random integer in [0..Range-1] |

**Note:** For more random functions, see [Math Reference](stdlib_math.md#random-functions).

### Example: Random Record Selection
```pascal
// Select random records from a file
var
  f: IwbFile;
  i, count, randomIndex: Integer;
  rec: IwbMainRecord;
begin
  Randomize();  // Initialize once

  f := FileByIndex(0);
  count := RecordCount(f);

  for i := 1 to 10 do begin
    randomIndex := Random(count);
    rec := RecordByIndex(f, randomIndex);
    AddMessage(Format('Random %d: %s', [i, rec.EditorID]));
  end;
end;
```

## TObject Methods

Base class methods available on all objects:

| Method | Signature | Description |
|--------|-----------|-------------|
| `ClassName` | `ClassName(): string` | Get class name |
| `ClassType` | `ClassType(): TClass` | Get class type |
| `ClassParent` | `ClassParent(): TClass` | Get parent class |
| `InheritsFrom` | `InheritsFrom(AClass: TClass): Boolean` | Test inheritance |
| `InstanceSize` | `InstanceSize(): Integer` | Size in bytes |

---

[← Back to Standard Library Overview](stdlib_home.md) | [Next: File Operations →](stdlib_files.md)

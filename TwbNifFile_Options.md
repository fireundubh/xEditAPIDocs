# Options

## Syntax

```pascal
function Options(ANifFile: TwbNifFile): Byte; // Get
procedure Options(ANifFile: TwbNifFile; AValue: Byte); // Set
```

## Description

Gets or sets NIF file processing options as a set of flags. Options control various aspects of NIF file serialization and optimization.

Available option flags:
- **nfoCollapseLinkArrays** (1): Collapse link arrays during save to reduce file size
- **nfoRemoveUnusedStrings** (2): Remove unused strings from the string palette during save

Options are stored as a byte where each bit represents a flag. Multiple options can be combined using bitwise OR.

These options primarily affect save operations and can help optimize the output file size and structure.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ANifFile | TwbNifFile | The NIF file object |
| AValue | Byte | The options value to set (for setter) |

## Returns

Returns the current options as a byte (for getter).

## Example

```pascal
var
  nif: TwbNifFile;
  opts: Byte;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\architecture\farmhouse\farmhouse01.nif');

    // Get current options
    opts := nif.Options;
    AddMessage('Current options: ' + IntToStr(opts));

    // Enable both optimization options
    // nfoCollapseLinkArrays = 1
    // nfoRemoveUnusedStrings = 2
    nif.Options := 1 or 2; // = 3

    // Save with optimizations
    nif.SaveToFile('meshes\architecture\farmhouse\farmhouse01_optimized.nif');
  finally
    nif.Free;
  end;
end;
```

## Example (Setting Individual Flags)

```pascal
var
  nif: TwbNifFile;
  opts: Byte;
const
  nfoCollapseLinkArrays = 1;
  nfoRemoveUnusedStrings = 2;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\chest\chestcommon.nif');

    // Start with no options
    opts := 0;

    // Add collapse link arrays option
    opts := opts or nfoCollapseLinkArrays;

    // Conditionally add unused strings removal
    if true then
      opts := opts or nfoRemoveUnusedStrings;

    nif.Options := opts;

    nif.SaveToFile('meshes\clutter\chest\chestcommon_optimized.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_InternalUpdates](TwbNifFile_InternalUpdates.md)
- [TdfElement_SaveToFile](TdfElement_SaveToFile.md)
- [TwbNifFile_NifVersion](TwbNifFile_NifVersion.md)

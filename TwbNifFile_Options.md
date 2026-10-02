# Options

## Syntax

```pascal
property Options: Byte;
```

Access via: `nifFile.Options` (read) or `nifFile.Options := value` (write)

## Description

Gets or sets NIF file processing options as a set of flags. Options control various aspects of NIF file serialization and optimization.

The registered constants are ordinals, not bit masks: `nfoCollapseLinkArrays` is 0 and `nfoRemoveUnusedStrings` is 1. The property stores the set as a byte. Bit 0 (value 1) is collapse link arrays. Bit 1 (value 2) is remove unused strings. Assign a set, which shifts those ordinals into bits, or assign the byte directly.

- **nfoCollapseLinkArrays**: Collapse link arrays during save to remove None links
- **nfoRemoveUnusedStrings**: Remove unused strings from the string palette during save

A new file starts with `nfoRemoveUnusedStrings` set (byte value 2). Collapse runs only while `InternalUpdates` is also true.

These options primarily affect save operations and can help optimize the output file size and structure.

This is a read/write property.

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

    // Set both flags. Do not assign the ordinal constants by themselves:
    // nfoCollapseLinkArrays is 0, not the bit value 1.
    nif.Options := [nfoCollapseLinkArrays, nfoRemoveUnusedStrings];

    // Save with optimizations
    nif.SaveToFile('meshes\architecture\farmhouse\farmhouse01_optimized.nif');
  finally
    nif.Free;
  end;
end;
```

## Example (Set both flags)

```pascal
var
  nif: TwbNifFile;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\chest\chestcommon.nif');

    nif.Options := [nfoCollapseLinkArrays, nfoRemoveUnusedStrings];

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

# NifVersion

## Syntax

```pascal
property NifVersion: Integer;
```

Access via: `nifFile.NifVersion` (read) or `nifFile.NifVersion := value` (write)

## Description

Gets or sets the NIF file version, which determines the file format and feature support. Different games use different NIF versions.

NIF versions are represented by enumeration values:
- **nfTES3** (1): Morrowind
- **nfTES4** (2): Oblivion
- **nfFO3** (3): Fallout 3 / New Vegas
- **nfTES5** (4): Skyrim
- **nfSSE** (5): Skyrim Special Edition
- **nfFO4** (6): Fallout 4

The version affects:
- Block types available
- Data structure layouts
- Feature support (e.g., shader types, vertex formats)
- File serialization format

When creating a new NIF, always set the version first before adding blocks. When loading a NIF, the version is automatically detected from the file header.

This is a read/write property.

## Returns

Returns the NIF version as an integer (for getter).

## Example

```pascal
var
  nif: TwbNifFile;
  version: Integer;
  versionName: string;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\armor\iron\ironarmor.nif');

    // Get the version
    version := nif.NifVersion;

    case version of
      1: versionName := 'Morrowind';
      2: versionName := 'Oblivion';
      3: versionName := 'Fallout 3';
      4: versionName := 'Skyrim';
      5: versionName := 'Skyrim SE';
      6: versionName := 'Fallout 4';
      else versionName := 'Unknown';
    end;

    AddMessage('NIF Version: ' + versionName + ' (' + IntToStr(version) + ')');
  finally
    nif.Free;
  end;
end;
```

## Example (Creating Version-Specific NIF)

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    // Set version for Skyrim Special Edition
    nif.NifVersion := 5; // nfSSE

    // Now we can add SSE-specific blocks
    rootNode := nif.AddBlock('BSFadeNode');
    rootNode.ElementByPath['Name'].EditValue := 'Scene Root';

    nif.SaveToFile('meshes\test\sse_mesh.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_Create](TwbNifFile_Create.md)
- [TwbNifFile_Header](TwbNifFile_Header.md)
- [TwbNifBlock_IsNiObject](TwbNifBlock_IsNiObject.md)

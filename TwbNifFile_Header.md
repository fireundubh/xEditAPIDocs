# Header

## Syntax

```pascal
property Header: TwbNifBlock;
```

Access via: `nifFile.Header`

## Description

Returns the header block of the NIF file. The header contains metadata about the file including version information, block count, string tables, and other file-level data.

The header is always the first block in a NIF file (index 0) and contains essential information:
- NIF version numbers
- Block type names table
- Block count
- String palette (in newer versions)
- Export info and metadata
- Root node references

You typically don't need to modify the header directly as it's automatically managed by the TwbNifFile class, but you can read its values to understand the file structure.

This is a read-only property.

## Returns

Returns the header block (always block index 0).

## Example

```pascal
var
  nif: TwbNifFile;
  header: TwbNifBlock;
  numBlocks: Integer;
  exportInfo: string;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\actors\character\character assets\skeleton.nif');

    // Get the header block
    header := nif.Header;

    if Assigned(header) then begin
      // Read header information
      numBlocks := header.ElementByPath['Num Blocks'].NativeValue;
      AddMessage('File contains ' + IntToStr(numBlocks) + ' blocks');

      // Get export info
      exportInfo := header.ElementByPath['Export Info'].EditValue;
      if exportInfo <> '' then
        AddMessage('Export Info: ' + exportInfo);

      // Get version string
      AddMessage('Version String: ' + header.ElementByPath['Version'].EditValue);
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_Footer](TwbNifFile_Footer.md)
- [TwbNifFile_BlocksCount](TwbNifFile_BlocksCount.md)
- [TwbNifFile_NifVersion](TwbNifFile_NifVersion.md)
- [TwbNifFile_Blocks](TwbNifFile_Blocks.md)

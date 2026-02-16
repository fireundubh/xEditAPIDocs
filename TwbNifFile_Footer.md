# Footer

## Syntax

```pascal
property Footer: TwbNifBlock;
```

Access via: `nifFile.Footer`

## Description

Returns the footer block of the NIF file if one exists. The footer contains additional metadata and root node references in certain NIF versions.

Footers are only present in some NIF versions (primarily Oblivion and later). The footer typically contains:
- Root node references
- Number of root nodes
- Additional metadata

If the NIF file doesn't have a footer (older versions like Morrowind), this may return nil or an empty block. The presence and structure of footers varies by NIF version.

This is a read-only property.

## Returns

Returns the footer block if present, or nil/empty block if the version doesn't use footers.

## Example

```pascal
var
  nif: TwbNifFile;
  footer: TwbNifBlock;
  numRoots: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\architecture\whiterun\wrterrain01.nif');

    // Get the footer block
    footer := nif.Footer;

    if Assigned(footer) then begin
      // Read footer information
      numRoots := footer.NativeValues['Num Roots'];
      AddMessage('Footer indicates ' + IntToStr(numRoots) + ' root nodes');
    end else
      AddMessage('This NIF version does not use a footer');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_Header](TwbNifFile_Header.md)
- [TwbNifFile_BlocksCount](TwbNifFile_BlocksCount.md)
- [TwbNifFile_NifVersion](TwbNifFile_NifVersion.md)

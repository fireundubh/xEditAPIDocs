# Footer

## Syntax

```pascal
property Footer: TwbNifBlock;
```

Access via: `nifFile.Footer`

## Description

Returns the footer block. It is not part of `Blocks` and is not nil after the file is created or loaded. The footer stores the `Roots` array of root-node references.

This is a read-only property.

## Returns

Returns the footer block.

## Example

```pascal
var
  nif: TwbNifFile;
  footer: TwbNifBlock;
  roots: TdfElement;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\architecture\whiterun\wrterrain01.nif');

    footer := nif.Footer;

    if Assigned(footer) then begin
      roots := footer.Elements['Roots'];
      if Assigned(roots) then
        AddMessage('Footer indicates ' + IntToStr(roots.Count) + ' root nodes');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_Header](TwbNifFile_Header.md)
- [TwbNifFile_BlocksCount](TwbNifFile_BlocksCount.md)
- [TwbNifFile_NifVersion](TwbNifFile_NifVersion.md)

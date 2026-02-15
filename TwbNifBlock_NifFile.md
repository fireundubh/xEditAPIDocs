# NifFile

## Syntax

```pascal
function NifFile(ABlock: TwbNifBlock): TwbNifFile;
```

## Description

Returns the parent TwbNifFile object that contains this block. This provides access to the overall NIF file structure and all other blocks in the file.

Every block in a NIF file is part of a TwbNifFile container. This property allows you to navigate from any individual block back to the file level, where you can access file-wide operations, other blocks, the header, footer, and file version information.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The NIF block to query |

## Returns

Returns the TwbNifFile object that contains this block.

## Example

```pascal
var
  nif: TwbNifFile;
  block: TwbNifBlock;
  parentFile: TwbNifFile;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\actors\character\character assets\skeleton.nif');

    // Get a specific block
    block := nif.BlockByType('NiNode');

    // Navigate back to the parent file
    parentFile := NifFile(block);

    // Now we can access file-level properties
    AddMessage('NIF Version: ' + IntToStr(Ord(parentFile.NifVersion)));
    AddMessage('Total blocks: ' + IntToStr(parentFile.BlocksCount));
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_Create](TwbNifFile_Create.md)
- [TwbNifFile_NifVersion](TwbNifFile_NifVersion.md)
- [TwbNifFile_BlocksCount](TwbNifFile_BlocksCount.md)
- [TwbNifFile_Header](TwbNifFile_Header.md)

# StringsCount

## Syntax

```pascal
function StringsCount(ABlock: TwbNifBlock): Integer;
```

## Description

Returns the number of indexed string elements in this NIF block. Indexed strings are string values that are referenced by index from a string table, commonly used in NIF files to reduce file size by storing frequently used strings only once.

Different NIF versions handle strings differently:
- Older versions store strings inline within blocks
- Newer versions (Skyrim/Fallout 4) use a string palette where strings are indexed by number

Indexed strings are commonly used for:
- Block names (for scene graph nodes)
- Texture file paths
- Material names
- Shader parameter names

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The NIF block to query |

## Returns

Returns the count of indexed string elements in this block.

## Example

```pascal
var
  nif: TwbNifFile;
  block: TwbNifBlock;
  i, j: Integer;
  strElement: TdfElement;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\actors\dragon\character assets\skeleton.nif');

    for i := 0 to nif.BlocksCount - 1 do begin
      block := nif.Blocks[i];

      if StringsCount(block) > 0 then begin
        AddMessage(Format('Block %d (%s) has %d indexed strings:',
          [i, BlockType(block), StringsCount(block)]));

        for j := 0 to StringsCount(block) - 1 do begin
          strElement := block.Strings[j];
          AddMessage('  String[' + IntToStr(j) + ']: ' + strElement.EditValue);
        end;
      end;
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_Strings](TwbNifBlock_Strings.md)
- [TwbNifBlock_RefsCount](TwbNifBlock_RefsCount.md)
- [TwbNifBlock_BlockType](TwbNifBlock_BlockType.md)

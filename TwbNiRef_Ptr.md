# Ptr

## Syntax

```pascal
function Ptr(ANiRef: TwbNiRef): Boolean;
```

## Description

Returns whether this reference is a NiPtr (pointer to following blocks) rather than a NiRef (reference to preceding blocks).

In NIF files, there are two types of block references:
- **NiRef**: Points backward to blocks that appear earlier in the file (lower block indices)
- **NiPtr**: Points forward to blocks that appear later in the file (higher block indices)

This distinction is important for understanding the NIF file structure and block dependencies. Most references are NiRefs pointing to previously defined blocks, but some specialized cases use NiPtr to point forward in the block list.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ANiRef | TwbNiRef | The NIF reference element |

## Returns

Returns True if this is a NiPtr (forward pointer), False if this is a NiRef (backward reference).

## Example

```pascal
var
  nif: TwbNifFile;
  block: TwbNifBlock;
  ref: TwbNiRef;
  i: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\bucket01.nif');

    block := nif.Blocks[0];

    for i := 0 to block.RefsCount - 1 do begin
      ref := block.Refs[i];
      if Ptr(ref) then
        AddMessage('Reference ' + IntToStr(i) + ' is a forward pointer (NiPtr)')
      else
        AddMessage('Reference ' + IntToStr(i) + ' is a backward reference (NiRef)');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNiRef_Template](TwbNiRef_Template.md)
- [TwbNifBlock_RefsCount](TwbNifBlock_RefsCount.md)
- [TwbNifBlock_Refs](TwbNifBlock_Refs.md)

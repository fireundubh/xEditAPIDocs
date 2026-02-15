# Template

## Syntax

```pascal
function Template(ANiRef: TwbNiRef): string;
```

## Description

Returns the template string that defines what type of NIF block this reference can point to. The template specifies the expected block type inheritance, allowing validation of block references within the NIF file structure.

In NIF files, references (NiRef) are pointers to other blocks in the file. Each reference has a template that constrains which block types are valid targets. For example, a NiNode's Children array might have references with template "NiAVObject", meaning the children must be NiAVObject blocks or blocks that inherit from NiAVObject (like NiNode, NiTriShape, etc.).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ANiRef | TwbNiRef | The NIF reference element |

## Returns

Returns the template string defining the expected block type for this reference.

## Example

```pascal
var
  nif: TwbNifFile;
  block: TwbNifBlock;
  childRef: TwbNiRef;
  i: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\armor\iron\ironarmor.nif');

    // Get first block
    block := nif.Blocks[0];

    // Check what type of blocks its references expect
    for i := 0 to block.RefsCount - 1 do begin
      childRef := block.Refs[i];
      AddMessage('Reference ' + IntToStr(i) + ' expects: ' + Template(childRef));
      // Example output: "Reference 0 expects: NiAVObject"
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNiRef_Ptr](TwbNiRef_Ptr.md)
- [TwbNifBlock_IsNiObject](TwbNifBlock_IsNiObject.md)
- [TwbNifBlock_BlockType](TwbNifBlock_BlockType.md)

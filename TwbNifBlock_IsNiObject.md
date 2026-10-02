# IsNiObject

## Syntax

```pascal
function IsNiObject(ATemplate: string): Boolean;
function IsNiObject(ATemplate: string; AInherited: Boolean): Boolean;
```

**Access via:** `block.IsNiObject(ATemplate)` or `block.IsNiObject(ATemplate, Inherited)`

## Description

Tests whether a NIF block matches a specific block type or inherits from it. This is essential for type checking in NIF manipulation, as NIF uses an inheritance-based type system.

The method can check for exact type matches or include inheritance checking. When inheritance checking is enabled, it returns True if the block is of the specified type OR inherits from that type. For example, checking if a BSTriShape IsNiObject("NiAVObject", True) returns True because BSTriShape inherits from NiAVObject.

The check walks the block type's ancestors. `NiTriShape` matches `NiTriBasedGeom` and `NiAVObject`. `BSTriShape` matches `NiAVObject`, not `NiTriShape` or `NiTriBasedGeom`. `NiTriStrips` is a separate `NiTriBasedGeom` descendant.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ATemplate | string | The block type name to test against |
| AInherited | Boolean | Optional. If True, check inheritance; if False, require exact match. Default is True |

## Returns

Returns True if the block matches the template (exactly or through inheritance), False otherwise.

## Example

```pascal
var
  nif: TwbNifFile;
  block: TwbNifBlock;
  i: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\architecture\solitude\sroofcorner01.nif');

    // Find all renderable objects (anything that inherits from NiAVObject)
    for i := 0 to nif.BlocksCount - 1 do begin
      block := nif.Blocks[i];

      if block.IsNiObject('NiAVObject', True) then
        AddMessage('Renderable block: ' + block.BlockType);
    end;

    // Check for exact type match
    block := nif.BlockByType('BSTriShape');
    if Assigned(block) then begin
      if block.IsNiObject('BSTriShape', False) then
        AddMessage('Exact match: BSTriShape');

      if block.IsNiObject('NiAVObject', True) then
        AddMessage('Inherits from NiAVObject');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_BlockType](TwbNifBlock_BlockType.md)
- [TwbNifBlock_ChildByType](TwbNifBlock_ChildByType.md)
- [TwbNifFile_BlockByType](TwbNifFile_BlockByType.md)
- [TwbNiRef_Template](TwbNiRef_Template.md)

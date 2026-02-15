# IsNiObject

## Syntax

```pascal
function IsNiObject(ABlock: TwbNifBlock; ATemplate: string): Boolean;
function IsNiObject(ABlock: TwbNifBlock; ATemplate: string; AInherited: Boolean): Boolean;
```

## Description

Tests whether a NIF block matches a specific block type or inherits from it. This is essential for type checking in NIF manipulation, as NIF uses an inheritance-based type system.

The function can check for exact type matches or include inheritance checking. When inheritance checking is enabled, it returns True if the block is of the specified type OR inherits from that type. For example, checking if a BSTriShape IsNiObject("NiAVObject", True) returns True because BSTriShape inherits from NiAVObject.

Common NIF inheritance chains:
- NiObject (base for all blocks)
  - NiAVObject (base for visible objects)
    - NiNode (scene graph nodes)
    - NiTriBasedGeom (base for geometry)
      - NiTriShape (triangle-based meshes)
      - NiTriStrips (triangle strip meshes)
        - BSTriShape (Skyrim SE/FO4 geometry)

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The NIF block to test |
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

      if IsNiObject(block, 'NiAVObject', True) then
        AddMessage('Renderable block: ' + BlockType(block));
    end;

    // Check for exact type match
    block := nif.BlockByType('BSTriShape');
    if Assigned(block) then begin
      if IsNiObject(block, 'BSTriShape', False) then
        AddMessage('Exact match: BSTriShape');

      if IsNiObject(block, 'NiTriShape', True) then
        AddMessage('Inherits from NiTriShape');
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

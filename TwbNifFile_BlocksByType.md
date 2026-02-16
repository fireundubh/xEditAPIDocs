# BlocksByType

## Syntax

```pascal
procedure BlocksByType(ABlockType: string; AList: TList);
procedure BlocksByType(ABlockType: string; AList: TList; AInherited: Boolean);
```

Access via: `nifFile.BlocksByType(BlockType, List)` or `nifFile.BlocksByType(BlockType, List, Inherited)`

## Description

Populates a TList with all blocks of the specified type found in the NIF file. This method searches through the entire block list and adds matching blocks to the provided list.

The function can search for exact type matches or include inheritance. When inheritance checking is enabled, it includes all blocks that are of the specified type or inherit from it.

This is useful for:
- Finding all geometry in a file (NiTriBasedGeom with inheritance)
- Locating all shader properties
- Finding all nodes of a specific type
- Processing multiple blocks of the same type

The list must be created before calling this method and should be freed by the caller.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlockType | string | The block type to search for |
| AList | TList | The list to populate with matching blocks |
| AInherited | Boolean | Optional. If True, include inherited types; if False, exact match only. Default is False |

## Returns

This is a procedure (no return value). Results are added to the provided list.

## Example

```pascal
var
  nif: TwbNifFile;
  geometryList: TList;
  shaderList: TList;
  i: Integer;
  block: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  geometryList := TList.Create;
  shaderList := TList.Create;
  try
    nif.LoadFromFile('meshes\architecture\whiterun\wrbuildings\wrinnsolab01.nif');

    // Find all geometry blocks (including derived types)
    nif.BlocksByType('NiTriBasedGeom', geometryList, True);

    AddMessage('Found ' + IntToStr(geometryList.Count) + ' geometry blocks:');
    for i := 0 to geometryList.Count - 1 do begin
      block := TwbNifBlock(geometryList[i]);
      AddMessage('  ' + block.BlockType);
    end;

    // Find all shader properties
    nif.BlocksByType('BSLightingShaderProperty', shaderList, False);

    AddMessage('Found ' + IntToStr(shaderList.Count) + ' shader properties');
  finally
    shaderList.Free;
    geometryList.Free;
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_BlockByType](TwbNifFile_BlockByType.md)
- [TwbNifFile_BlockByName](TwbNifFile_BlockByName.md)
- [TwbNifBlock_ChildrenByType](TwbNifBlock_ChildrenByType.md)
- [TwbNifFile_BlocksCount](TwbNifFile_BlocksCount.md)

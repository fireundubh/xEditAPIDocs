# ChildrenByType

## Syntax

```pascal
procedure ChildrenByType(ABlockType: string; AList: TList);
procedure ChildrenByType(ABlockType: string; AList: TList; AInherited: Boolean);
```

**Access via:** `block.ChildrenByType(ABlockType, AList)` or `block.ChildrenByType(ABlockType, AList, Inherited)`

## Description

Populates a TList with all child blocks of a specific type. This method searches the block's Children array and adds matching blocks to the provided list.

The method can search for exact type matches or include inheritance. When inheritance checking is enabled, it includes all children that are of the specified type or inherit from it. This is useful for finding all geometry (anything inheriting from NiTriBasedGeom) or all visible objects (anything inheriting from NiAVObject).

The list must be created before calling this method and should be freed by the caller. The list contains references to existing blocks, not copies.

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
  rootNode: TwbNifBlock;
  geometryList: TList;
  i: Integer;
  child: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  geometryList := TList.Create;
  try
    nif.LoadFromFile('meshes\architecture\solitude\scastle01.nif');

    rootNode := nif.RootNode;

    if Assigned(rootNode) then begin
      // Find all geometry children (including inherited types)
      rootNode.ChildrenByType('NiTriBasedGeom', geometryList, True);

      AddMessage('Found ' + IntToStr(geometryList.Count) + ' geometry children:');
      for i := 0 to geometryList.Count - 1 do begin
        child := TwbNifBlock(geometryList[i]);
        AddMessage('  ' + child.BlockType);
      end;
    end;
  finally
    geometryList.Free;
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_ChildByType](TwbNifBlock_ChildByType.md)
- [TwbNifBlock_PropertiesByType](TwbNifBlock_PropertiesByType.md)
- [TwbNifBlock_ExtraDatasByType](TwbNifBlock_ExtraDatasByType.md)
- [TwbNifBlock_IsNiObject](TwbNifBlock_IsNiObject.md)

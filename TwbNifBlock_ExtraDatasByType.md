# ExtraDatasByType

## Syntax

```pascal
procedure ExtraDatasByType(ABlockType: string; AList: TList);
procedure ExtraDatasByType(ABlockType: string; AList: TList; AInherited: Boolean);
```

**Access via:** `block.ExtraDatasByType(ABlockType, AList)` or `block.ExtraDatasByType(ABlockType, AList, Inherited)`

## Description

Populates a TList with all extra data blocks of a specific type attached to this block. Extra data stores metadata and custom information on scene nodes and geometry.

The method can search for exact type matches or include inheritance. When inheritance checking is enabled, it includes all extra data blocks that are of the specified type or inherit from it.

Common extra data types to search for:
- "NiStringExtraData" - String metadata
- "NiIntegerExtraData" - Integer values
- "NiFloatExtraData" - Floating-point values
- "BSXFlags" - Bethesda behavior flags
- "BSBehaviorGraphExtraData" - Animation behavior graph
- "BSInvMarker" - Inventory marker

The list must be created before calling this method and should be freed by the caller.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlockType | string | The extra data type to search for |
| AList | TList | The list to populate with matching extra data blocks |
| AInherited | Boolean | Optional. If True, include inherited types; if False, exact match only. Default is False |

## Returns

This is a procedure (no return value). Results are added to the provided list.

## Example

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
  stringDataList: TList;
  i: Integer;
  extraData: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  stringDataList := TList.Create;
  try
    nif.LoadFromFile('meshes\actors\character\character assets\skeleton.nif');

    rootNode := nif.RootNode;

    if Assigned(rootNode) then begin
      // Find all string extra data
      rootNode.ExtraDatasByType('NiStringExtraData', stringDataList, False);

      AddMessage('Found ' + IntToStr(stringDataList.Count) + ' string extra data blocks:');
      for i := 0 to stringDataList.Count - 1 do begin
        extraData := TwbNifBlock(stringDataList[i]);
        AddMessage('  Name: ' + extraData.ElementByPath['Name'].EditValue);
        AddMessage('  Data: ' + extraData.ElementByPath['String Data'].EditValue);
      end;
    end;
  finally
    stringDataList.Free;
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_ExtraDataByType](TwbNifBlock_ExtraDataByType.md)
- [TwbNifBlock_ExtraDataByName](TwbNifBlock_ExtraDataByName.md)
- [TwbNifBlock_PropertiesByType](TwbNifBlock_PropertiesByType.md)
- [TwbNifBlock_AddExtraData](TwbNifBlock_AddExtraData.md)

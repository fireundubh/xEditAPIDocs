# ExtraDataByName

## Syntax

```pascal
function ExtraDataByName(AName: string): TwbNifBlock;
```

**Access via:** `block.ExtraDataByName(AName)`

## Description

Finds and returns an extra data block attached to this block by searching for a matching name. Returns nil if no extra data with the specified name is found.

Extra data blocks have a Name field that identifies their purpose. This method searches through all extra data attached to the block and returns the first one with a matching name. This is the primary way to locate specific extra data blocks.

Common extra data names:
- "PRISM" - Bethesda's legacy metadata
- "BSBehaviorGraphExtraData" - Animation behavior graph
- "BSBound" - Bounding box data
- "BSInvMarker" - Inventory marker position
- "Tangent space (binormal & tangent vectors)" - TES4 tangent data

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AName | string | The name of the extra data to find |

## Returns

Returns the extra data block with the matching name, or nil if not found.

## Example

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
  bsxFlags: TwbNifBlock;
  invMarker: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\armor\iron\ironarmor.nif');

    rootNode := nif.RootNode;

    if Assigned(rootNode) then begin
      // Look for BSX flags
      bsxFlags := rootNode.ExtraDataByName('BSX');
      if Assigned(bsxFlags) then
        AddMessage('Found BSXFlags: ' + IntToStr(bsxFlags.NativeValues['Integer Data']));

      // Look for inventory marker
      invMarker := rootNode.ExtraDataByName('INV');
      if Assigned(invMarker) then begin
        AddMessage('Found inventory marker');
        AddMessage('  Rotation: ' + invMarker.EditValues['Rotation']);
      end else
        AddMessage('No inventory marker found');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_ExtraDataByType](TwbNifBlock_ExtraDataByType.md)
- [TwbNifBlock_ExtraDatasByType](TwbNifBlock_ExtraDatasByType.md)
- [TwbNifBlock_PropertyByName](TwbNifBlock_PropertyByName.md)
- [TwbNifBlock_AddExtraData](TwbNifBlock_AddExtraData.md)

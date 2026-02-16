# BlockByName

## Syntax

```pascal
function BlockByName(ABlockName: string): TwbNifBlock;
```

Access via: `nifFile.BlockByName(Name)`

## Description

Finds and returns the first block with the specified name. Returns nil if no block with that name is found.

Many NIF blocks (particularly nodes) have a Name field that identifies them. This method searches through all blocks and returns the first one whose Name field matches the specified string.

This is particularly useful for:
- Finding skeleton bones by name
- Locating named scene graph nodes
- Finding specific collision objects
- Accessing named markers or attachment points

The search is case-sensitive and matches the exact string.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlockName | string | The name to search for |

## Returns

Returns the first block with the matching name, or nil if none found.

## Example

```pascal
var
  nif: TwbNifFile;
  boneBlock: TwbNifBlock;
  markerBlock: TwbNifBlock;
  transform: TdfElement;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\actors\character\character assets\skeleton.nif');

    // Find a specific bone
    boneBlock := nif.BlockByName('NPC Spine2 [Spn2]');

    if Assigned(boneBlock) then begin
      AddMessage('Found bone: ' + boneBlock.BlockType);

      // Access the bone's transform
      transform := boneBlock.Elements['Transform'];
      if Assigned(transform) then
        AddMessage('Transform: ' + transform.EditValue);
    end else
      AddMessage('Bone not found');

    // Find a marker
    markerBlock := nif.BlockByName('FireplaceMarker');

    if Assigned(markerBlock) then
      AddMessage('Found marker at block index ' + IntToStr(markerBlock.Index));
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_BlockByType](TwbNifFile_BlockByType.md)
- [TwbNifFile_BlocksByType](TwbNifFile_BlocksByType.md)
- [TwbNifBlock_ExtraDataByName](TwbNifBlock_ExtraDataByName.md)
- [TwbNifBlock_PropertyByName](TwbNifBlock_PropertyByName.md)

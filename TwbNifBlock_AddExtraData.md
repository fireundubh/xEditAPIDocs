# AddExtraData

## Syntax

```pascal
function AddExtraData(ABlockType: string): TwbNifBlock;
```

**Access via:** `block.AddExtraData(ABlockType)`

## Description

Adds a new extra data block to this NIF block and returns the created block. Extra data blocks store additional metadata and custom information attached to scene nodes and geometry.

Extra data blocks are used for various purposes:
- **NiStringExtraData**: Store text metadata (names, tags, flags)
- **NiIntegerExtraData**: Store integer values
- **NiFloatExtraData**: Store floating-point values
- **BSXFlags**: Bethesda-specific flags for object behavior
- **BSBehaviorGraphExtraData**: Animation behavior graph data
- **BSInvMarker**: Inventory marker position data

The method creates a new extra data block, adds it to the NIF file, and links it to the parent block's Extra Data list.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlockType | string | The type of extra data block to create (e.g., "NiStringExtraData", "BSXFlags") |

## Returns

Returns the newly created extra data block.

## Example

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
  bsxFlags: TwbNifBlock;
  stringData: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\bucket01.nif');

    rootNode := nif.BlockByType('NiNode');

    if Assigned(rootNode) then begin
      // Add BSXFlags to control object behavior
      bsxFlags := rootNode.AddExtraData('BSXFlags');
      bsxFlags.NativeValues['Integer Data'] := 2; // Static

      // Add custom string metadata
      stringData := rootNode.AddExtraData('NiStringExtraData');
      stringData.EditValues['Name'] := 'MyCustomTag';
      stringData.EditValues['String Data'] := 'CustomValue';

      AddMessage('Added extra data to root node');
      nif.SaveToFile('meshes\clutter\bucket01_modified.nif');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_ExtraDataByName](TwbNifBlock_ExtraDataByName.md)
- [TwbNifBlock_ExtraDataByType](TwbNifBlock_ExtraDataByType.md)
- [TwbNifBlock_AddChild](TwbNifBlock_AddChild.md)
- [TwbNifBlock_AddProperty](TwbNifBlock_AddProperty.md)

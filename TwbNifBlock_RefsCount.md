# RefsCount

## Syntax

```pascal
property RefsCount: Integer;
```

Access via: `block.RefsCount`

## Description

Returns the number of block references (NiRef and NiPtr elements) contained in this NIF block. Block references are pointers to other blocks in the NIF file and are used to build the scene graph hierarchy and link related data.

References are fundamental to NIF file structure. They create relationships between blocks such as:
- Parent-child relationships in the scene graph (NiNode children)
- Links to properties (materials, shaders, textures)
- Links to extra data (metadata, custom data)
- Links to skinning, collision, and animation data

## Returns

Returns the count of block references in this block.

## Example

```pascal
var
  nif: TwbNifFile;
  node: TwbNifBlock;
  i: Integer;
  childRef: TwbNiRef;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\chest\chestcommon.nif');

    node := nif.BlockByType('NiNode');

    if Assigned(node) then begin
      AddMessage('Node has ' + IntToStr(node.RefsCount) + ' references');

      // Iterate through all references
      for i := 0 to node.RefsCount - 1 do begin
        childRef := node.Refs[i];
        AddMessage('Reference ' + IntToStr(i) + ': ' + childRef.Template);
      end;
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_Refs](TwbNifBlock_Refs.md)
- [TwbNiRef_Template](TwbNiRef_Template.md)
- [TwbNiRef_Ptr](TwbNiRef_Ptr.md)
- [TwbNifBlock_StringsCount](TwbNifBlock_StringsCount.md)

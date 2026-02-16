# Refs

## Syntax

```pascal
property Refs[Index: Integer]: TwbNiRef;
```

Access via: `block.Refs[index]`

## Description

Returns a specific block reference (NiRef or NiPtr element) from this block by index. References are indexed from 0 to RefsCount-1 and represent pointers to other blocks in the NIF file.

This indexed property provides access to the individual reference elements within a block. Each reference can be inspected to determine its template (expected block type) and whether it's a forward or backward pointer.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Index | Integer | Zero-based index of the reference to retrieve |

## Returns

Returns the TwbNiRef element at the specified index.

## Example

```pascal
var
  nif: TwbNifFile;
  node: TwbNifBlock;
  childRef: TwbNiRef;
  refValue: Integer;
  i: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\furniture\throne01.nif');

    node := nif.BlockByType('NiNode');

    if Assigned(node) then begin
      AddMessage('Examining ' + IntToStr(node.RefsCount) + ' references:');

      for i := 0 to node.RefsCount - 1 do begin
        childRef := node.Refs[i];

        AddMessage(Format('Ref[%d]: Template=%s, IsPtr=%s',
          [i, childRef.Template, BoolToStr(childRef.Ptr, True)]));

        // Get the actual block index this reference points to
        refValue := childRef.NativeValue;
        if refValue >= 0 then
          AddMessage('  Points to block ' + IntToStr(refValue));
      end;
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_RefsCount](TwbNifBlock_RefsCount.md)
- [TwbNiRef_Template](TwbNiRef_Template.md)
- [TwbNiRef_Ptr](TwbNiRef_Ptr.md)
- [TwbNifBlock_Strings](TwbNifBlock_Strings.md)

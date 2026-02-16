# Strings

## Syntax

```pascal
property Strings[Index: Integer]: TdfElement;
```

Access via: `block.Strings[index]`

## Description

Returns a specific indexed string element from this block by index. Indexed strings are accessed from 0 to StringsCount-1 and represent string values that use the NIF string palette system.

The returned TdfElement can be used to read or modify the string value using its EditValue or NativeValue properties. In newer NIF versions (Skyrim SE, Fallout 4), these strings are stored in a centralized string palette and referenced by index to reduce file size.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Index | Integer | Zero-based index of the string element to retrieve |

## Returns

Returns the TdfElement representing the indexed string at the specified position.

## Example

```pascal
var
  nif: TwbNifFile;
  node: TwbNifBlock;
  nameStr: TdfElement;
  i: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\actors\draugr\character assets\skeleton.nif');

    // Find all named nodes in the skeleton
    for i := 0 to nif.BlocksCount - 1 do begin
      node := nif.Blocks[i];

      if (node.BlockType = 'NiNode') and (node.StringsCount > 0) then begin
        // Get the name string (usually first indexed string)
        nameStr := node.Strings[0];
        AddMessage('Found node: ' + nameStr.EditValue);
      end;
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_StringsCount](TwbNifBlock_StringsCount.md)
- [TwbNifBlock_Refs](TwbNifBlock_Refs.md)
- [TdfElement_EditValue](TdfElement_EditValue.md)
- [TdfElement_NativeValue](TdfElement_NativeValue.md)

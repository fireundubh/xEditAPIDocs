# NifBlockList

## Syntax

```pascal
function NifBlockList(AData: TBytes; AList: TStrings): Boolean;
```

## Description

Extracts all block type names from a NIF (NetImmerse File Format) mesh file and adds them to a string list. This function parses the NIF binary structure and identifies all node and block types present in the mesh.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AData | TBytes | The raw binary data of the NIF file |
| AList | TStrings | The string list to receive the block type names |

## Returns

Returns True if the NIF was successfully parsed and block names were extracted, False otherwise.

## Example

```pascal
var
  nifData: TBytes;
  blockList: TStringList;
begin
  blockList := TStringList.Create;
  try
    nifData := ResourceOpenData('', 'meshes\armor\iron\ironarmor.nif');

    if NifBlockList(nifData, blockList) then
      AddMessage('NIF contains ' + IntToStr(blockList.Count) + ' blocks');
  finally
    blockList.Free;
  end;
end;
```

## See Also

- [NifTextureList](IwbResource_NifTextureList.md)
- [NifTextureListResource](IwbResource_NifTextureListResource.md)

# NifBlockList

## Syntax

```pascal
function NifBlockList(AData: TBytes; AList: TStrings): Boolean;
```

## Description

Clears `AList` and fills it with one line per block in a NIF. Each line is `Name=BlockType`, and that line's `Objects` value is the block index. A nil list returns False and is not written. A NIF that does not load returns False after the list has been cleared.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AData | TBytes | The raw binary data of the NIF file |
| AList | TStrings | List cleared and filled with `Name=BlockType` lines |

## Returns

True when the NIF loaded. False when `AList` is nil or the NIF did not load. An empty block list can still return True.

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

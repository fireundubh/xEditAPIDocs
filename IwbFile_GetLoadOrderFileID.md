# GetLoadOrderFileID

## Syntax

```pascal
function GetLoadOrderFileID(AFile: IwbFile): string;
```

## Description

Returns `AFile`'s load-order module slot as a string.

A full plugin is two hex digits (`00`, `0B`). A medium plugin is `FD` plus a space plus two hex digits. A light plugin is `FE` plus a space plus three hex digits.

This is the load-order slot, not a file FormID. [RecordByFormID](IwbFile_RecordByFormID.md) does not take this string.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose slot is needed |

## Returns

The slot string. Returns `-1` when `AFile` is not a file. A file that has no slot raises.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByIndex(0);
  if Assigned(f) then
    AddMessage(GetLoadOrderFileID(f));
end;
```

## See Also

- [GetLoadOrder](IwbFile_GetLoadOrder.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)

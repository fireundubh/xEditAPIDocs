# GetNewFormID

## Syntax

```pascal
function GetNewFormID(AFile: IwbFile): Cardinal;
```

## Description

Allocates the next free FormID in `AFile`. For Oblivion and later, it advances the header's next-object id.

The result is a file FormID for `AFile`, not a load-order FormID. The object id stays inside the range for the file's module type: 24 bits for a full plugin, 16 for a medium plugin, 12 for a light plugin. An update plugin raises instead of allocating one.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file that will own the new FormID |

## Returns

The new file FormID, or `0` when `AFile` is not a file.

## Example

```pascal
var
  f: IwbFile;
  newFormID: Cardinal;
begin
  f := FileByIndex(0);
  if Assigned(f) then
    newFormID := GetNewFormID(f);
end;
```

## See Also

- [FormID](IwbMainRecord_FormID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)

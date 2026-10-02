# LoadOrderFormIDtoFileFormID

## Syntax

```pascal
function LoadOrderFormIDtoFileFormID(AFile: IwbFile; AFormID: Integer): Cardinal;
```

## Description

Converts a load-order FormID to a file FormID for `AFile`.

The module prefix of `AFormID` is a load-order slot. The result replaces it with that plugin's file id in `AFile`: a full plugin's index in the master list, or a light or medium plugin's index among masters of the same type. When the prefix is `AFile`, the result uses `AFile`'s own file id. Pass the result to [RecordByFormID](IwbFile_RecordByFormID.md). Do not pass the load-order FormID to that lookup.

A hardcoded FormID is returned unchanged. A prefix that is not `AFile` and not one of its masters raises.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file the FormID is converted for |
| AFormID | Integer | Load-order FormID |

## Returns

The file FormID as a Cardinal. If `AFile` is not a file, the result is unassigned.

## Example

```pascal
var
  f: IwbFile;
  fileFormID: Cardinal;
  r: IwbMainRecord;
begin
  f := FileByIndex(0);
  if Assigned(f) and Assigned(e) then begin
    fileFormID := LoadOrderFormIDtoFileFormID(f, GetLoadOrderFormID(e));
    r := RecordByFormID(f, fileFormID, True);
    if Assigned(r) then
      AddMessage(Name(r));
  end;
end;
```

## See Also

- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [FormID](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)

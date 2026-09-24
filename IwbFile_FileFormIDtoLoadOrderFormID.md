# FileFormIDtoLoadOrderFormID

## Syntax

```pascal
function FileFormIDtoLoadOrderFormID(AFile: IwbFile; AFormID: Integer): Cardinal;
```

## Description

Converts `AFormID`, relative to `AFile`, to a Form ID relative to the current load order

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file containing the form ID |
| AFormID | Integer | The file-relative form ID to convert |

## Returns

Returns the load-order-relative form ID as a Cardinal value.

## Example

```pascal
// File FormID to load-order FormID. Do not pass the result to RecordByFormID.
// That lookup wants the file FormID. See LoadOrderFormIDtoFileFormID.
var
  f: IwbFile;
  loadOrderFormID: Cardinal;
begin
  if Assigned(e) then begin
    f := GetFile(e);
    if Assigned(f) then begin
      loadOrderFormID := FileFormIDtoLoadOrderFormID(f, FormID(e));
      AddMessage(IntToHex(loadOrderFormID, 8));
    end;
  end;
end;
```

## See Also

- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [FormID](IwbMainRecord_FormID.md)
- [GetFile](IwbElement_GetFile.md)
- [LoadOrderFormIDtoFileFormID](IwbFile_LoadOrderFormIDtoFileFormID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)



# RecordByHexFormID

## Syntax

```pascal
function RecordByHexFormID(AFormID: string): IwbMainRecord;
```

## Description

Retrieves a main record by its complete FormID in hexadecimal string format. The function searches through all loaded files to find the record with the matching FormID. The FormID should include both the file index and record ID components.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFormID | string | The FormID as a hexadecimal string (e.g., '05001234' or 'FE000ABC') |

## Returns

Returns an IwbMainRecord interface for the record with the matching FormID, or nil if not found.

## Example

```pascal
var
  record: IwbMainRecord;
begin
  // Find a record with FormID 05001234
  record := RecordByHexFormID('05001234');

  if Assigned(record) then
    AddMessage('Found record: ' + record.Name);
end;
```

## See Also

- [RecordByFormID](IwbFile_RecordByFormID.md)
- [FileByLoadOrderFileID](Global_FileByLoadOrderFileID.md)

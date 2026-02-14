# RecordByIndex

## Syntax

```pascal
function RecordByIndex(AFile: IwbFile; AIndex: Integer): IwbMainRecord;
```

## Description

Returns the main record at the specified zero-based index within the file.

This function accesses the Records property by index, providing array-style access to all main records in the file. The implementation includes a bounds check and returns nil if the index is >= RecordCount. Index order is determined by the file's internal record organization. Use RecordCount to get the valid index range (0 to RecordCount-1).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to retrieve the record from |
| AIndex | Integer | The zero-based index of the record in the file |

## Returns

Returns the IwbMainRecord at the specified index.

## Example

```pascal
f := FileByName('Skyrim.esm');
r := RecordByIndex(f, 0);   // --> DoorMarker [STAT:00000001]
```

## See Also

- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md)
- [RecordCount](IwbFile_RecordCount.md)



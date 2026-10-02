# RecordByIndex

## Syntax

```pascal
function RecordByIndex(AFile: IwbFile; AIndex: Integer): IwbMainRecord;
```

## Description

Returns the main record at `AIndex` in `AFile`.

The index is zero-based and runs through [RecordCount](IwbFile_RecordCount.md). The records are the file's own main records, ordered by FormID. Groups and the file header are not in this list.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to read |
| AIndex | Integer | Zero-based index, from 0 through `RecordCount(AFile) - 1` |

## Returns

The main record at that index. The result is unassigned when `AIndex` is negative, `AIndex` is not less than [RecordCount](IwbFile_RecordCount.md), or `AFile` is not a file.

## Example

```pascal
var
  f: IwbFile;
  r: IwbMainRecord;
begin
  f := FileByName('Skyrim.esm');
  if Assigned(f) then begin
    r := RecordByIndex(f, 0);
    if Assigned(r) then
      AddMessage(Name(r));
  end;
end;
```

## See Also

- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md)
- [RecordCount](IwbFile_RecordCount.md)

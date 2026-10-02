# RecordCount

## Syntax

```pascal
function RecordCount(AFile: IwbFile): Integer;
```

## Description

Returns how many main records `AFile` contains.

The count is the records [RecordByIndex](IwbFile_RecordByIndex.md) can return. Groups and the file header are not included.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to count |

## Returns

The number of main records, or `0` when `AFile` is not a file.

## Example

```pascal
var
  f: IwbFile;
  r: IwbMainRecord;
  i: Integer;
begin
  f := FileByName('Skyrim.esm');
  if Assigned(f) then
    for i := 0 to Pred(RecordCount(f)) do begin
      r := RecordByIndex(f, i);
      if Assigned(r) then
        AddMessage(Name(r));
    end;
end;
```

## See Also

- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)

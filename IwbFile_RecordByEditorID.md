# RecordByEditorID

## Syntax

```pascal
function RecordByEditorID(AFile: IwbFile; AEditorID: string): IwbMainRecord;
```

## Description

Looks up a main record by EditorID.

The comparison is case-insensitive. The search starts in `AFile`. If `AFile` has no match, it continues through `AFile`'s masters, from the last master toward the first. The record that comes back can be stored in a master rather than in `AFile`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to search, then its masters |
| AEditorID | string | EditorID to find |

## Returns

The matching main record, or nil when `AFile` and its masters have no such EditorID. If `AFile` is not a file, the result is unassigned.

## Example

```pascal
var
  f: IwbFile;
  r: IwbMainRecord;
begin
  f := FileByName('Skyrim.esm');
  if Assigned(f) then begin
    r := RecordByEditorID(f, 'ActionIdle');
    if Assigned(r) then
      AddMessage(Name(r));
  end;
end;
```

## See Also

- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)
- [RecordCount](IwbFile_RecordCount.md)

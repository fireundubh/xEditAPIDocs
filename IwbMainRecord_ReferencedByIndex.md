# ReferencedByIndex

## Syntax

```pascal
function ReferencedByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns the record at the specified index in the list of records referencing this record.

This function accesses the ReferencedBy property by index, providing array-style access to all records that contain FormID fields pointing to this record. The order is determined internally and may not be meaningful. Use ReferencedByCount to get the valid index range. Returns nil for invalid indices. Ensure BuildRef has been called to populate the reference tracking.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to get incoming references from |
| AIndex | integer | The zero-based index in the array of referencing records |

## Returns

Returns the IwbMainRecord at the specified index that references this record.

## Example

```pascal
for i := 0 to Pred(ReferencedByCount(e)) do
begin
	r := ReferencedByIndex(e, i);
  AddMessage(Name(e) + ' is linked to by an element in: ' + Name(r));
end;
```

## See Also

- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)
- [BuildRef](IwbElement_BuildRef.md)
- [LinksTo](IwbElement_LinksTo.md)



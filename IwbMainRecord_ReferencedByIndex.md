# ReferencedByIndex

## Syntax

```pascal
function ReferencedByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns record at `AIndex` in array of records linking to `ARecord`

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
- [ReferencesCount](IwbMainRecord_ReferencesCount.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)



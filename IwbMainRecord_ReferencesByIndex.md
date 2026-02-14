# ReferencesByIndex

## Syntax

```pascal
function ReferencesByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns record at `AIndex` in array of records linked to by `ARecord`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to get outgoing references from |
| AIndex | integer | The zero-based index in the array of referenced records |

## Returns

Returns the IwbMainRecord at the specified index that this record references.

## Example

```pascal
for i := 0 to Pred(ReferencesCount(e)) do
begin
	r := ReferencesByIndex(e, i);
  AddMessage(Name(e) + ' contains element linking to: ' + Name(r));
end;
```

## See Also

- [ReferencesCount](IwbMainRecord_ReferencesCount.md)
- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)
- [UpdateRefs](IwbMainRecord_UpdateRefs.md)
- [LinksTo](IwbElement_LinksTo.md)



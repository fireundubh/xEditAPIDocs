# ReferencesByIndex

## Syntax

```pascal
function ReferencesByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns record at `AIndex` in array of records linked to by `ARecord`

## Example

```pascal
for i := 0 to Pred(ReferencesCount(e)) do
begin
	r := ReferencesByIndex(e, i);
  AddMessage(Name(e) + ' contains element linking to: ' + Name(r));
end;
```

## See Also

- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)
- [ReferencesCount](IwbMainRecord_ReferencesCount.md)

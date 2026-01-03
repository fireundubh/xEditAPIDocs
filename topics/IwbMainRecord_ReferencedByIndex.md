# ReferencedByIndex

## Syntax

```pascal
function ReferencedByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns record at `AIndex` in array of records linking to `ARecord`

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



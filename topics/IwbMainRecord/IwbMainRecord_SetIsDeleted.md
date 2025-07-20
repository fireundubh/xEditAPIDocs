# SetIsDeleted

## Syntax

```pascal
procedure SetIsDeleted(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Deleted when `AFlag` is `True` and otherwise when `AFlag` is `False`

## Example

```pascal
SetIsDeleted(e, True);
if GetIsDeleted(e) then
	AddMessage(Name(e) + ' is flagged as Deleted');
  
SetIsDeleted(e, False);
if GetIsDeleted(e) then
	AddMessage(Name(e) + ' is not flagged as Deleted');
```

## See Also

- [GetIsDeleted](IwbMainRecord_GetIsDeleted.md)

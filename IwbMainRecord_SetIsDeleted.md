# SetIsDeleted

## Syntax

```pascal
procedure SetIsDeleted(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Deleted when `AFlag` is `True` and otherwise when `AFlag` is `False`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Deleted flag on |
| AFlag | boolean | Whether to set (True) or clear (False) the Deleted flag |

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



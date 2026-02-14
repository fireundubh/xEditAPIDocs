# SetIsVisibleWhenDistant

## Syntax

```pascal
procedure SetIsVisibleWhenDistant(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Visible When Distant when `AFlag` is `True` and otherwise when `AFlag` is `False`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Visible When Distant flag on |
| AFlag | boolean | Whether to set (True) or clear (False) the Visible When Distant flag |

## Example

```pascal
SetIsVisibleWhenDistant(e, True);
if GetIsVisibleWhenDistant(e) then
	AddMessage(Name(e) + ' is flagged as Visible When Distant');
  
SetIsVisibleWhenDistant(e, False);
if GetIsVisibleWhenDistant(e) then
	AddMessage(Name(e) + ' is not flagged as Visible When Distant');
```

## See Also

- [GetIsVisibleWhenDistant](IwbMainRecord_GetIsVisibleWhenDistant.md)



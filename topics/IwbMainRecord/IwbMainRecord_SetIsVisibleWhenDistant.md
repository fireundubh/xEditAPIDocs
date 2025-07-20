# SetIsVisibleWhenDistant

## Syntax

```pascal
procedure SetIsVisibleWhenDistant(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Visible When Distant when `AFlag` is `True` and otherwise when `AFlag` is `False`

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

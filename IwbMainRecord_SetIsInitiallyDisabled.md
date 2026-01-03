# SetIsInitiallyDisabled

## Syntax

```pascal
procedure SetIsInitiallyDisabled(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Initially Disabled when `AFlag` is `True` and otherwise when `AFlag` is `False`

## Example

```pascal
SetIsInitiallyDisabled(e, True);
if GetIsInitiallyDisabled(e) then
	AddMessage(Name(e) + ' is flagged as Initially Disabled');
  
SetIsInitiallyDisabled(e, False);
if GetIsInitiallyDisabled(e) then
	AddMessage(Name(e) + ' is not flagged as Initially Disabled');
```

## See Also

- [GetIsInitiallyDisabled](IwbMainRecord_GetIsInitiallyDisabled.md)



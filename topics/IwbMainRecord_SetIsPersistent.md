# SetIsPersistent

## Syntax

```pascal
procedure SetIsPersistent(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Persistent when `AFlag` is `True` and otherwise when `AFlag` is `False`

## Example

```pascal
SetIsPersistent(e, True);
if GetIsPersistent(e) then
	AddMessage(Name(e) + ' is flagged as Persistent');
  
SetIsPersistent(e, False);
if GetIsPersistent(e) then
	AddMessage(Name(e) + ' is not flagged as Persistent');
```

## See Also

- [GetIsPersistent](IwbMainRecord_GetIsPersistent.md)



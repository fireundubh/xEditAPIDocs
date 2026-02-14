# SetIsPersistent

## Syntax

```pascal
procedure SetIsPersistent(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Persistent when `AFlag` is `True` and otherwise when `AFlag` is `False`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Persistent flag on |
| AFlag | boolean | Whether to set (True) or clear (False) the Persistent flag |

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



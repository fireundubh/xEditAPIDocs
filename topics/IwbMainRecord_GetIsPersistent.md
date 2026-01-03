# GetIsPersistent

## Syntax

```pascal
function GetIsPersistent(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is flagged as Persistent

## Example

```pascal
if GetIsPersistent(e) then
	AddMessage(Name(e) + ' is flagged as Persistent');
```

## See Also

- [SetIsPersistent](IwbMainRecord_SetIsPersistent.md)



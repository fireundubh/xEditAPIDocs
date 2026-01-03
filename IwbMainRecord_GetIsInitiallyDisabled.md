# GetIsInitiallyDisabled

## Syntax

```pascal
function GetIsInitiallyDisabled(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is flagged as Initially Disabled

## Example

```pascal
if GetIsInitiallyDisabled(e) then
	AddMessage(Name(e) + ' is flagged as Initially Disabled');
```

## See Also

- [SetIsInitiallyDisabled](IwbMainRecord_SetIsInitiallyDisabled.md)



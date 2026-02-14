# GetIsInitiallyDisabled

## Syntax

```pascal
function GetIsInitiallyDisabled(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is flagged as Initially Disabled

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check the Initially Disabled flag on |

## Returns

Returns `True` if the record is flagged as Initially Disabled, `False` otherwise.

## Example

```pascal
if GetIsInitiallyDisabled(e) then
	AddMessage(Name(e) + ' is flagged as Initially Disabled');
```

## See Also

- [SetIsInitiallyDisabled](IwbMainRecord_SetIsInitiallyDisabled.md)



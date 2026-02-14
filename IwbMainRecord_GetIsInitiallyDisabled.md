# GetIsInitiallyDisabled

## Syntax

```pascal
function GetIsInitiallyDisabled(ARecord: IwbMainRecord): boolean;
```

## Description

Checks whether the record has the Initially Disabled flag set in its record header.

This function retrieves the IsInitiallyDisabled property, which checks a flag bit specific to reference records (REFR, ACHR, etc.). Initially disabled references are inactive when the cell loads but can be enabled by scripts or quests. Returns false for invalid records or non-reference record types. This is primarily used for placed references in the game world.

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
- [GetIsDeleted](IwbMainRecord_GetIsDeleted.md)
- [GetIsPersistent](IwbMainRecord_GetIsPersistent.md)
- [GetIsVisibleWhenDistant](IwbMainRecord_GetIsVisibleWhenDistant.md)



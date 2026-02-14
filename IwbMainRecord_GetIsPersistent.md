# GetIsPersistent

## Syntax

```pascal
function GetIsPersistent(ARecord: IwbMainRecord): boolean;
```

## Description

Checks whether the record has the Persistent flag set in its record header.

This function retrieves the IsPersistent property, which checks a flag bit specific to reference records (REFR, ACHR, etc.). Persistent references remain loaded in memory even when their cell is not active, making them accessible to scripts at all times. Returns false for invalid records or non-reference record types. Essential for references that need to be referenced by scripts or quests from anywhere.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check the Persistent flag on |

## Returns

Returns `True` if the record is flagged as Persistent, `False` otherwise.

## Example

```pascal
if GetIsPersistent(e) then
	AddMessage(Name(e) + ' is flagged as Persistent');
```

## See Also

- [SetIsPersistent](IwbMainRecord_SetIsPersistent.md)



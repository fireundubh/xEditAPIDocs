# Master

## Syntax

```pascal
function Master(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the master record that this record directly overrides.

This function retrieves the Master property, which returns the immediate parent record in the override chain (the record from a higher-priority file that this record modifies). Returns nil if this record is itself a master (not an override of anything). For records with multiple levels of overrides, this returns only the direct parent, not the original master.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The overriding record to get the master from |

## Returns

Returns the master IwbMainRecord that is overridden, or Nil if the record is not an override.

## Example

```pascal
mr := Master(e);
if not Assigned(mr) then
	AddMessage(Name(e) + ' is not an overriding record');
```

## See Also

- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)
- [IsMaster](IwbMainRecord_IsMaster.md)
- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [OverrideCount](IwbMainRecord_OverrideCount.md)
- [OverrideByIndex](IwbMainRecord_OverrideByIndex.md)



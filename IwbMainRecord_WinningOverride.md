# WinningOverride

## Syntax

```pascal
function WinningOverride(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the final overriding record in the current load order.

This function retrieves the WinningOverride property, which returns the last record in the override chain (the one with the highest load order that modifies this FormID). If the record has no overrides, returns the record itself. This is the "active" version of the record that the game will use. Unlike HighestOverrideOrSelf, this always returns the absolute last override regardless of load order position.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the winning override from |

## Returns

Returns the last loaded overriding IwbMainRecord, or the record itself if no overrides exist.

## Example

```pascal
o := WinningOverride(e);
AddMessage(GetFileName(GetFile(o)));  // Output: [09] MyPlugin.esp
```

## See Also

- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md)
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)
- [Master](IwbMainRecord_Master.md)
- [OverrideByIndex](IwbMainRecord_OverrideByIndex.md)



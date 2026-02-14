# HighestOverrideOrSelf

## Syntax

```pascal
function HighestOverrideOrSelf(ARecord: IwbMainRecord; AMaxLoadOrder: integer): IwbMainRecord;
```

## Description

Returns an overriding record for `ARecord` that loads last nearest to `AMaxLoadOrder`, or the record itself

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to find the highest override for |
| AMaxLoadOrder | integer | The maximum load order to search up to |

## Returns

Returns the highest override record up to the specified load order, or the record itself if no override exists.

## Example

```pascal
mr := HighestOverrideOrSelf(e, 0);
AddMessage(GetFileName(GetFile(mr)));  // Output: [00] Fallout4.esm

mr := HighestOverrideOrSelf(e, 6);
AddMessage(GetFileName(GetFile(mr)));  // Output: [00] Fallout4.esm

mr := HighestOverrideOrSelf(e, 7);
AddMessage(GetFileName(GetFile(mr)));  // Output: [07] Unofficial Fallout 4 Patch.esp
```

## See Also

- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)
- [OverrideByIndex](IwbMainRecord_OverrideByIndex.md)



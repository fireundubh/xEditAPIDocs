# HighestOverrideOrSelf

## Syntax

```pascal
function HighestOverrideOrSelf(ARecord: IwbMainRecord; AMaxLoadOrder: integer): IwbMainRecord;
```

## Description

Returns an overriding record for `ARecord` that loads last nearest to `AMaxLoadOrder`, or the record itself

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



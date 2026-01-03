# WinningOverride

## Syntax

```pascal
function WinningOverride(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the last loaded overriding record for `ARecord`, or the record itself

Unlike [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md), the return value of this function cannot be constrained to a specific load order index. This function will always return the *last* loaded overriding record for the current load order, or the record itself.

## Example

```pascal
o := WinningOverride(e);
AddMessage(GetFileName(GetFile(o)));  // Output: [09] MyPlugin.esp
```

## See Also

- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)



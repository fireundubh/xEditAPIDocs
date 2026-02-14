# wbSimpleRecords

## Syntax

```pascal
function wbSimpleRecords: Boolean;
```

## Description

Returns whether simple records mode is enabled. In simple records mode, xEdit displays a simplified view of record structures, hiding complex internal details to improve performance and readability.

## Parameters

This function takes no parameters.

## Returns

Returns True if simple records mode is enabled, False otherwise.

## Example

```pascal
begin
  if wbSimpleRecords then
    AddMessage('Simple records mode is enabled')
  else
    AddMessage('Full record structure is displayed');
end;
```

## See Also

- [wbSettings](Global_wbSettings.md)

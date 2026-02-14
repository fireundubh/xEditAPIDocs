# wbTrackAllEditorID

## Syntax

```pascal
function wbTrackAllEditorID: Boolean;
```

## Description

Returns whether tracking of all Editor IDs is enabled. When enabled, xEdit maintains a comprehensive index of all Editor IDs across all loaded files for faster lookup and reference resolution.

## Parameters

This function takes no parameters.

## Returns

Returns True if Editor ID tracking is enabled, False otherwise.

## Example

```pascal
begin
  if wbTrackAllEditorID then
    AddMessage('All Editor IDs are being tracked')
  else
    AddMessage('Limited Editor ID tracking');
end;
```

## See Also

- [wbSettings](Global_wbSettings.md)

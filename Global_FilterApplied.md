# FilterApplied

## Syntax

```pascal
function FilterApplied: Boolean;
```

## Description

Returns whether a filter is currently applied to the navigation tree view. This function checks if the user interface is currently showing a filtered view of records.

## Parameters

This function takes no parameters.

## Returns

Returns True if a filter is currently applied, False otherwise.

## Example

```pascal
begin
  if FilterApplied then
    AddMessage('A filter is currently active')
  else
    AddMessage('No filter is applied');
end;
```

## See Also

- [ApplyFilter](Global_ApplyFilter.md)
- [RemoveFilter](Global_RemoveFilter.md)

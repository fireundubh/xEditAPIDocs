# RemoveFilter

## Syntax

```pascal
procedure RemoveFilter;
```

## Description

Removes the currently applied filter from the navigation tree view, restoring the full unfiltered display of all records. This function clears the active record selection and refreshes the view.

## Parameters

This function takes no parameters.

## Returns

This function does not return a value.

## Example

```pascal
begin
  if FilterApplied then begin
    RemoveFilter;
    AddMessage('Filter removed, showing all records');
  end;
end;
```

## See Also

- [ApplyFilter](Global_ApplyFilter.md)
- [FilterApplied](Global_FilterApplied.md)

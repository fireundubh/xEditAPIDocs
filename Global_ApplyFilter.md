# ApplyFilter

## Syntax

```pascal
procedure ApplyFilter;
```

## Description

Applies the currently configured filter to the navigation tree view without showing the filter configuration dialog. This function sets a preset flag to skip the user interface and directly applies the filter settings.

## Parameters

This function takes no parameters.

## Returns

This function does not return a value.

## Example

```pascal
begin
  // Configure filter settings beforehand, then apply
  ApplyFilter;
  AddMessage('Filter applied to records');
end;
```

## See Also

- [RemoveFilter](Global_RemoveFilter.md)
- [FilterApplied](Global_FilterApplied.md)

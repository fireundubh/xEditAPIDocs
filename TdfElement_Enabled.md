# TdfElement.Enabled

## Syntax

```pascal
property Enabled: Boolean;
```

## Description

Gets or sets whether this element is currently active and should be included in serialization.

The Enabled property controls whether an element participates in binary serialization and is visible for navigation. Optional or conditional fields in binary formats use this mechanism - when Enabled is False, the element is skipped during save operations and excluded from DataSize calculations.

Definitions can implement OnGetEnabled callbacks to determine enabled status dynamically based on other field values. For example, a version-specific field might only be enabled if the file version matches certain criteria.

Setting Enabled to False effectively removes the element from the binary output without destroying it, allowing it to be re-enabled later.

This property is read-write.

## Parameters

This property has no parameters.

## Returns

Returns True if the element is enabled and active, False otherwise.

## Example

```pascal
var
    element: TdfElement;
begin
    // Check if element is enabled
    if element.Enabled then
        AddMessage('Element is active')
    else
        AddMessage('Element is disabled');

    // Disable element
    element.Enabled := False;
end;
```

## See Also

- [TdfElement.ElementByName](TdfElement_ElementByName.md)
- [TdfElement.ElementByPath](TdfElement_ElementByPath.md)
- [TdfElement.DataSize](TdfElement_DataSize.md)
- [TdfElement.Count](TdfElement_Count.md)

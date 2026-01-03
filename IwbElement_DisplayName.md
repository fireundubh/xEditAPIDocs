# DisplayName

## Syntax

```pascal
function DisplayName(AElement: IwbElement): string;
```

## Description

Returns the display name of the element.

If the element has a specific display name, it returns that name. Otherwise, this function behaves identically to Name. This is useful for getting user-friendly names for elements in the interface.

## Example

```pascal
var
  element: IwbElement;
  name: string;
begin
  name := DisplayName(element);
  // Use the display name
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [BaseName](IwbElement_BaseName.md)
- [ShortName](IwbElement_ShortName.md)



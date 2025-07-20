# SetToDefault

## Syntax

```pascal
procedure SetToDefault(AElement: IwbElement);
```

## Description

Resets the element's data and adds missing fields if any.

This procedure restores an element to its default state and ensures all required fields are present.

## Example

```pascal
var
    element: IwbElement;
begin
    SetToDefault(element);
end;
```

## See Also

- [Check - IwbElement](IwbElement_Check.md)

# SetEditValue

## Syntax

```pascal
function SetEditValue(AElement: IwbElement; AValue: string): string;
```

## Description

Sets an element's value using a string representation.

Allows setting the value of an element using a string format. The function handles the conversion from string to the appropriate internal format for the element type.

## Example

```pascal
begin
  SetEditValue(element, '42');
end;
```

## See Also

- [IsEditable](IwbElement_IsEditable.md)



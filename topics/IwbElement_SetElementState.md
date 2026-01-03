# SetElementState

## Syntax

```pascal
function SetElementState(AElement: IwbElement; AState: TwbElementState): TwbElementState;
```

## Description

Modifies the internal state flags of an element.

Returns the previous state value before modification. Used to manipulate internal element states.

## Example

```pascal
var
    previousState: TwbElementState;
begin
    previousState := SetElementState(element, newState);
end;
```

## See Also

- [IsEditable](IwbElement_IsEditable.md)



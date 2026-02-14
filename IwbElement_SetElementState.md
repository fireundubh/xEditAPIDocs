# SetElementState

## Syntax

```pascal
function SetElementState(AElement: IwbElement; AState: TwbElementState): TwbElementState;
```

## Description

Modifies the internal state flags of an element.

Returns the previous state value before modification. Used to manipulate internal element states.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose state to modify |
| AState | TwbElementState | The new state to set |

## Returns

Returns the previous state value as a TwbElementState enumeration value.

## Example

```pascal
var
    previousState: TwbElementState;
begin
    previousState := SetElementState(element, newState);
end;
```

## See Also

- [GetElementState](IwbElement_GetElementState.md)
- [ClearElementState](IwbElement_ClearElementState.md)
- [IsEditable](IwbElement_IsEditable.md)



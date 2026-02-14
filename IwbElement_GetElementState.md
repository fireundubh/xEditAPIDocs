# GetElementState

## Syntax

```pascal
function GetElementState(AElement: IwbElement; AState: TwbElementState): TwbElementState;
```

## Description

Checks the internal flags of an element.

This function is used to query the current state flags of an element. It's particularly useful for determining various conditions about the element's current state.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the state from |
| AState | TwbElementState | The state flag to check |

## Returns

Returns the element state as a TwbElementState enumeration value.

## Example

```pascal
var
  element: IwbElement;
  state: TwbElementState;
begin
  state := GetElementState(element, esModified);
  // Check the state
end;
```

## See Also

- [SetElementState](IwbElement_SetElementState.md)
- [ClearElementState](IwbElement_ClearElementState.md)



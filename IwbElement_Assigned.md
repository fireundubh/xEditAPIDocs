# Assigned

## Syntax

```pascal
function Assigned(AElement: IwbElement): boolean;
```

## Description

Checks if an xEdit element reference is valid.

This is an overloaded version of Delphi's native `Assigned` function, specifically for `IwbElement` interfaces. Returns `true` if the element reference is not nil, `false` otherwise.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check for validity |

## Returns

Returns `true` if the element reference is not nil, `false` otherwise.

## Example

```pascal
var
  element: IwbElement;
begin
  if Assigned(element) then
    AddMessage('Element is valid')
  else
    AddMessage('Element is nil');
end;
```

## See Also

- [Check](IwbElement_Check.md)



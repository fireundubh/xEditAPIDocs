# JumpTo

## Syntax

```pascal
procedure JumpTo(AElement: IwbElement; ABackward: boolean);
```

## Description

Scrolls the xEdit window to show the specified element.

This procedure navigates the xEdit interface to display the specified element. The `ABackward` parameter determines the direction of history navigation.

## Example

```pascal
var
  element: IwbElement;
begin
  element := // ... get element reference
  JumpTo(element, false); // Navigate forward to element
end;
```

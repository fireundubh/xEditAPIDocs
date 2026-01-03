# IsInjected

## Syntax

```pascal
function IsInjected(AElement: IwbElement): boolean;
```

## Description

Determines if the element was injected by another plugin.

Returns `true` if the element was injected by another plugin rather than being part of the original plugin file. This is useful for identifying elements that were added through script or other external means.

## Example

```pascal
var
  element: IwbElement;
begin
  if IsInjected(element) then
    // Handle injected element
end;
```

## See Also

- [IsMaster](../IwbMainRecord/IwbMainRecord_IsMaster.md)
- [IsWinningOverride](../IwbMainRecord/IwbMainRecord_IsWinningOverride.md)

# LinksTo

## Syntax

```pascal
function LinksTo(AElement: IwbElement): IwbElement;
```

## Description

Returns the element that this element references.

For elements that contain references to other records (like FormIDs), this function returns the referenced element. Returns nil if the element doesn't reference anything or if the reference is invalid.

## Example

```pascal
var
  element: IwbElement;
  linkedElement: IwbElement;
begin
  linkedElement := LinksTo(element);
  if Assigned(linkedElement) then
    // Work with the referenced element
end;
```

## See Also

- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)



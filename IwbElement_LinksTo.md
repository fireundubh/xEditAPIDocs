# LinksTo

## Syntax

```pascal
function LinksTo(AElement: IwbElement): IwbElement;
```

## Description

Returns the element that this element references.

For elements that contain references to other records (like FormIDs), this function returns the referenced element. Returns nil if the element doesn't reference anything or if the reference is invalid.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the linked reference from |

## Returns

Returns the referenced element as an IwbElement interface, or nil if no reference exists.

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



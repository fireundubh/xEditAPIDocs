# CanContainFormIDs

## Syntax

```pascal
function CanContainFormIDs(AElement: IwbElement): boolean;
```

## Description

Determines if an element can contain form IDs.

This function accesses an internal property `CanContainFormIDs` which the internal implementation of BuildRef uses to skip processing certain descendant elements. While it will always return `True` if the element can contain form IDs, it's not guaranteed to return `False` if it can't.

## Example

```pascal
var
  element: IwbElement;
  canContain: boolean;
begin
  canContain := CanContainFormIDs(element);
  if canContain then
    // Process element for form IDs
end;
```

## See Also

- [LinksTo - IwbElement](IwbElement_LinksTo.md)

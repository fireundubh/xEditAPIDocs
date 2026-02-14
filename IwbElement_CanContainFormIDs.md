# CanContainFormIDs

## Syntax

```pascal
function CanContainFormIDs(AElement: IwbElement): boolean;
```

## Description

Determines if an element can contain form IDs.

This function accesses an internal property `CanContainFormIDs` which the internal implementation of BuildRef uses to skip processing certain descendant elements. While it will always return `True` if the element can contain form IDs, it's not guaranteed to return `False` if it can't.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check |

## Returns

Returns `true` if the element can contain form IDs. Note that a `false` result is not guaranteed to mean the element cannot contain form IDs.

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

- [LinksTo](IwbElement_LinksTo.md)



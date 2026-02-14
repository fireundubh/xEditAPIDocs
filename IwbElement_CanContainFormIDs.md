# CanContainFormIDs

## Syntax

```pascal
function CanContainFormIDs(AElement: IwbElement): boolean;
```

## Description

Checks whether the element's definition allows it to contain FormID references.

This function retrieves the CanContainFormIDs property, which returns true if the element's structure can include FormID fields (either directly or in descendant elements). This is an optimization hint used by BuildRef to skip branches that cannot contain references. Returns false for simple value types (integers, strings, etc.) but may return false negatively (false when it actually can). Returns false for invalid elements.

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
- [BuildRef](IwbElement_BuildRef.md)
- [FormID](IwbMainRecord_FormID.md)



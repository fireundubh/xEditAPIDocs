# LinksTo

## Syntax

```pascal
function LinksTo(AElement: IwbElement): IwbElement;
```

## Description

Resolves and returns the element or record that this element references.

This function retrieves the LinksTo property, which resolves FormID references to their target records or elements. For FormID fields, it returns the IwbMainRecord being referenced. For other reference types, it may return the appropriate target element. Returns nil (unassigned) if the element is not a reference type, the reference is invalid, or the target cannot be found.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the linked reference from |

## Returns

Returns the referenced element as an IwbElement interface, or nil if no reference exists.

## Example

```pascal
var
  baseElement, referencedBase: IwbElement;
  baseRecord: IwbMainRecord;
begin
  // Get the base object reference from a placed object
  baseElement := ElementByPath(e, 'NAME');
  if Assigned(baseElement) then begin
    baseRecord := LinksTo(baseElement) as IwbMainRecord;
    if Assigned(baseRecord) then
      AddMessage('References: ' + EditorID(baseRecord));
  end;
end;
```

## See Also

- [CanContainFormIDs](IwbElement_CanContainFormIDs.md)
- [BuildRef](IwbElement_BuildRef.md)
- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)



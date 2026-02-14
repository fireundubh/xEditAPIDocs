# ContainingMainRecord

## Syntax

```pascal
function ContainingMainRecord(AElement: IwbElement): IwbMainRecord;
```

## Description

Returns the IwbMainRecord that owns this element in the record hierarchy.

This function retrieves the ContainingMainRecord property, which traverses up the element tree to find the nearest IwbMainRecord ancestor. For subrecords and nested elements, this returns the record they belong to. For main records, this returns the record itself. Returns nil for elements not part of a main record (like file headers or groups). Useful for navigating from field-level elements to their owning record.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the containing main record for |

## Returns

Returns the containing main record as an IwbMainRecord interface.

## Example

```pascal
var
  element: IwbElement;
  mainRecord: IwbMainRecord;
begin
  mainRecord := ContainingMainRecord(element);
  if Assigned(mainRecord) then
    // Work with the main record
end;
```

## See Also

- [GetContainer](IwbElement_GetContainer.md)
- [GetFile](IwbElement_GetFile.md)
- [EditorID](IwbMainRecord_EditorID.md)
- [FormID](IwbMainRecord_FormID.md)



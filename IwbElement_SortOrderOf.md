# SortOrderOf

## Syntax

```pascal
function SortOrderOf(AElement: IwbElement): integer;
```

## Description

Returns the sort order index of an element within its parent container. This is the definition-level index that identifies a specific member slot in a record or struct, and is the value needed for the AIndex parameter of ElementAssign.

For main record children, the sort order corresponds to the member definition index (e.g., EDID might be 0, FULL might be 12). For array elements, it reflects the element's position. Returns -1 if the element is not assigned.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the sort order of |

## Returns

Returns the sort order index of the element, or -1 if not assigned.

## Example

```pascal
// Example 1: Get sort order for use with ElementAssign
var
  rec, sourceRec: IwbMainRecord;
  fullName, sourceName: IwbElement;
  sortOrder: integer;
begin
  rec := RecordByFormID(FileByIndex(0), $00012345, True);
  sourceRec := RecordByFormID(FileByIndex(0), $00067890, True);
  if Assigned(rec) and Assigned(sourceRec) then begin
    sourceName := ElementBySignature(sourceRec, 'FULL');
    if Assigned(sourceName) then begin
      sortOrder := SortOrderOf(sourceName);
      AddMessage(Format('FULL sort order: %d', [sortOrder]));
      // Use sort order to copy the element to another record
      ElementAssign(rec, sortOrder, sourceName, False);
    end;
  end;
end;

// Example 2: Compare sort orders of different elements
var
  edid, full: IwbElement;
begin
  if Assigned(e) then begin
    edid := ElementBySignature(e, 'EDID');
    full := ElementBySignature(e, 'FULL');
    if Assigned(edid) and Assigned(full) then
      AddMessage(Format('EDID sort order: %d, FULL sort order: %d',
        [SortOrderOf(edid), SortOrderOf(full)]));
  end;
end;
```

## See Also

- [IndexOf](IwbContainer_IndexOf.md)
- [ElementAssign](IwbElement_ElementAssign.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)


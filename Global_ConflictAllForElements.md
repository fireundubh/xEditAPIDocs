# ConflictAllForElements

## Syntax

```pascal
function ConflictAllForElements(aElements: TList; aSiblingCompare: Boolean; aQuickCheck: Boolean): TConflictAll;
// or
function ConflictAllForElements(aElement1: IwbElement; aElement2: IwbElement; aSiblingCompare: Boolean; aQuickCheck: Boolean): TConflictAll;
```

## Description

Calculates the overall conflict level for a collection of elements or a pair of elements. This function analyzes how elements conflict with each other and returns the highest conflict level found. It supports both list-based and pair-based comparisons.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aElements | TList | A list of IwbElement interfaces to check for conflicts (3-parameter variant) |
| aElement1 | IwbElement | First element to compare (4-parameter variant) |
| aElement2 | IwbElement | Second element to compare (4-parameter variant) |
| aSiblingCompare | Boolean | Whether to compare elements as siblings |
| aQuickCheck | Boolean | If True, performs a faster but less thorough conflict check |

## Returns

Returns a TConflictAll enumeration value indicating the overall conflict level (caUnknown, caOnlyOne, caNoConflict, caConflictBenign, caOverride, caConflict, or caConflictCritical).

## Example

```pascal
var
  elementList: TList;
  conflictLevel: Integer;
  i: Integer;
begin
  elementList := TList.Create;
  try
    // Add elements to compare
    for i := 0 to FileCount - 1 do
      elementList.Add(Pointer(RecordByFormID(FileByIndex(i), $00012345)));

    conflictLevel := ConflictAllForElements(elementList, True, False);

    if conflictLevel = caConflict then
      AddMessage('Critical conflicts detected between elements');
  finally
    elementList.Free;
  end;
end;
```

## See Also

- [ConflictAllForMainRecord](Global_ConflictAllForMainRecord.md)
- [ConflictAllForNode](Global_ConflictAllForNode.md)

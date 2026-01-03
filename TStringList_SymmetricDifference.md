# TStringList.SymmetricDifference

## Syntax

```pascal
procedure AList1.SymmetricDifference(AList2: TStringList);
```

## Description

Executes a set symmetric difference operation on the `TStringList` object and modifies it in-place.

The operation is `Self := (Self - AList2) ∪ (AList2 - Self)`.

The list is automatically sorted and duplicates are set to ignore before the operation.

## Example

```pascal
list1.SymmetricDifference(list2);
```

## See Also

- [Difference](TStringList_Difference.md)
- [Intersection](TStringList_Intersection.md)
- [Union](TStringList_Union.md)

# TStringList.Difference

## Syntax

```pascal
procedure AList1.Difference(AList2: TStringList);
```

## Description

Executes a set difference operation on the `TStringList` object and modifies it in-place.

The operation is `Self := Self - AList2`.

The list is automatically sorted and duplicates are set to ignore before the operation.

## Example

```pascal
list1.Difference(list2);
```

## See Also

- [Intersection](TStringList_Intersection.md)
- [SymmetricDifference](TStringList_SymmetricDifference.md)
- [Union](TStringList_Union.md)

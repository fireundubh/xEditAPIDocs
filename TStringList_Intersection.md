# TStringList.Intersection

## Syntax

```pascal
procedure AList1.Intersection(AList2: TStringList);
```

## Description

Executes a set intersection operation on the `TStringList` object and modifies it in-place.

The operation is `Self := Self ∩ AList2`.

The list is automatically sorted and duplicates are set to ignore before the operation.

## Example

```pascal
list1.Intersection(list2);
```

## See Also

- [Difference](TStringList_Difference.md)
- [SymmetricDifference](TStringList_SymmetricDifference.md)
- [Union](TStringList_Union.md)

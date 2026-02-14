# Union

## Syntax

```pascal
procedure AList1.Union(AList2: TStringList);
```

## Description

Executes a set union operation on the `TStringList` object and modifies it in-place.

The operation is `Self := Self ∪ AList2`.

The list is automatically sorted and duplicates are set to ignore before the operation.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AList2 | TStringList | The string list to union with the current list |

## Example

```pascal
list1.Union(list2);
```

## See Also

- [Difference](TStringList_Difference.md)
- [Intersection](TStringList_Intersection.md)
- [SymmetricDifference](TStringList_SymmetricDifference.md)

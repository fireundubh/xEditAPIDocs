# TStringList.SymmetricDifference

## Syntax

```pascal
procedure SymmetricDifference(AList2: TStringList);
```

Access via: `list.SymmetricDifference(Other)`

## Description

Executes a set symmetric difference operation on the `TStringList` object and modifies it in-place.

The operation is `Self := (Self - AList2) ∪ (AList2 - Self)`.

The list is automatically sorted and duplicates are set to ignore before the operation.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AList2 | TStringList | The string list to compute symmetric difference with |

## Returns

Returns nothing. The list is modified in place.

## Example

```pascal
var
  list1, list2: TStringList;
begin
  list1 := TStringList.Create;
  try
    list2 := TStringList.Create;
    try
      list1.Add('Alpha');
      list1.Add('Beta');
      list2.Add('Beta');
      list2.Add('Gamma');
      list1.SymmetricDifference(list2);
    finally
      list2.Free;
    end;
  finally
    list1.Free;
  end;
end;
```

## See Also

- [Difference](TStringList_Difference.md)
- [Intersection](TStringList_Intersection.md)
- [Union](TStringList_Union.md)

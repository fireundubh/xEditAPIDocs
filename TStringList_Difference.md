# TStringList.Difference

## Syntax

```pascal
procedure Difference(AList2: TStringList);
```

Access via: `list.Difference(Other)`

## Description

Executes a set difference operation on the `TStringList` object and modifies it in-place.

The operation is `Self := Self - AList2`.

The list is automatically sorted and duplicates are set to ignore before the operation.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AList2 | TStringList | The string list to subtract from the current list |

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
      list1.Difference(list2);
    finally
      list2.Free;
    end;
  finally
    list1.Free;
  end;
end;
```

## See Also

- [Intersection](TStringList_Intersection.md)
- [SymmetricDifference](TStringList_SymmetricDifference.md)
- [Union](TStringList_Union.md)

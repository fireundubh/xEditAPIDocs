# ElementCount

## Syntax

```pascal
function ElementCount(AContainer: IwbContainer): integer;
```

## Description

Returns the total number of child elements currently in the container.

This function retrieves the ElementCount property, which returns the count of immediate children only (not recursive). Returns 0 for empty containers or invalid inputs. Use this to iterate through elements with ElementByIndex, or to check if a container has any children. Does not include elements that could be added but haven't been yet.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to count elements in |

## Returns

Returns the total number of elements as an integer.

## Example

```pascal
var
  count: integer;
begin
  count := ElementCount(container);
  AddMessage('Container has ' + IntToStr(count) + ' elements');
end;
```

## See Also

- [AdditionalElementCount](IwbContainer_AdditionalElementCount.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [LastElement](IwbContainer_LastElement.md)



# EnumValues

## Syntax

```pascal
function EnumValues(AElement: IwbElement): string;
```

## Description

Retrieves the names of set enum values for an element.

For elements that represent a set of named enum values, this function returns a space-separated string containing all the names of values that are currently set.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get enum values from |

## Returns

Returns a space-separated string containing all the names of set enum values.

## Example

```pascal
var
  values: string;
begin
  values := EnumValues(enumElement);
  // Example result: "Value1 Value2 Value3"
end;
```

## See Also

- [SetEditValue](IwbElement_SetEditValue.md)


